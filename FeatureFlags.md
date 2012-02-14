On Feature Flags
================

During the last MonsterOnRails meetup we hit the topic auf feature management in larger development teams. [Michael Schäfermeier](http://about.me/mschae) presented
a new development process used at [BleacherReport](http://www.bleacherreport.com). They use the GitHub's forking and pull request mechanisms extensive.
When a developer starts working on a new ticket, he has to run through the following workflow:
- open the ticket in Lighthouse,
- fork the main repository,
- create a personal "ticket branch",
- implement the feature/fix,
- push the changes to her personal repository,
- and finally make a pull request.
To ease this handling of Git and Lighthouse, Winton Welsh developed
a wrapper for Git, called [gitcycle](https://github.com/winton/gitcycle). The realized time savings are quite impressive; in a normal working day, Michael estimated
the savings to add up to nearly 40 minutes each developer.

Though the individual advantages are obvious, I was critical about the underlying process of feature- (respectively ticket-) branching.
I tend to sound a little black and white at times. I do not believe in general best practices; nearly everything in professional
software development [depends on the context](http://andreas-simon.blogspot.com/2011/02/photographic-testing-lessons-learned.html) of your team / project.
My opinion about feature branches is based on the articles of [Martin Fowler](http://www.martinfowler.com) on [feature branches](http://martinfowler.com/bliki/FeatureBranch.html),
[feature toggles](http://martinfowler.com/bliki/FeatureToggle.html), and [semantic merge conflicts](http://martinfowler.com/bliki/SemanticConflict.html).

The basic problem about feature branches is the deferred merging. It is a long known fact that the cost of bug fixing correlates to the length of the time span between bug creation and bug detection.
By creating a new branch for each new feature / ticket, you avoid early, continuous integration. When you have to integrate later on---before pushing and making the pull request---your knowledge is not as fresh as at the time writing the new code. Thus, it might be harder to fix merge conflicts---be it obvious conflicts detected by your version control system, or hidden
[semantic conflicts](http://martinfowler.com/bliki/SemanticConflict.html) with the code of your team mates. That is why I tend to prefer continuous integration in the trunk / master of your project.

When everybody commits to the same branch, you are faced with another problem: what do you with not-yet-finished features that you don't want to release yet? Martin Fowler advices
the use of [feature toggles](http://martinfowler.com/bliki/FeatureToggle.html), a.k.a feature flags. The idea is basically this: you create a single point in your code where you manage
the activation of your various features. Since features affect the GUI mainly, you insert conditional statements in your view code that displays the respective elements based
on the activation of the feature.

I want to give a small example: The [Envie gem](http://rubygems.org/gems/envie) makes it very easy to use feature toggles within Ruby on Rails applications. You define your environments
(e.g. development and test) inside `environment.rb`:

    development = Envie.development.with(:blog).with(:profile)
    test        = development.derive(:test)

That means, in the development environment, you activate the 'blog' and 'profile' features. The test environment enables the same features as the development environment. In any
other environment, none of the feature is active. To check whether a specific feature is enabled, just use the `feature()` method with a block of view code:

    <% feature(:blog) do %>
      <h2>My Blog</h2>
    <% end %>

By default, a feature is inactive. You have to enable a feature explicitly. When you rolled out the feature and detect some bug in production, it is easy to withdraw it by
switching off the feature toggle. When the feature is in production successfully for a while you should delete the feature toggle from your code; this prevents the pollution of your code by feature toggles.

At the time of presenting it, the new tool was in production for one week at BleacherReport. I am looking forward to Michael's long-term experiences.
