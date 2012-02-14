On Feature Flags
================

During the last MonsterOnRails meetup we hit the topic auf feature management in larger development
teams. [Michael Schäfermeier](http://about.me/mschae) presented
a new development process employed at [BleacherReport](http://www.bleacherreport.com), a very
large and successful sport site, built on user-generated content. They use
[GitHub's](http://www.github.com) forking and pull request mechanisms extensively.
When a developer starts to work on a new ticket, she has to adhere to the following workflow:
 1. open the ticket in Lighthouse,
 1. fork the main repository,
 1. create a personal "ticket branch",
 1. implement the feature/fix,
 1. merge in the latest HEAD from the master repository,
 1. push the changes to her personal repository,
 1. and finally make a pull request.
To ease the correct handling of Git and Lighthouse---especially for non-programmers---Winton
Welsh developed a wrapper for Git, called [gitcycle](https://github.com/winton/gitcycle). Gitcycle
automates the creation of a private branch from a ticket, and the correct publication of the new code.
The realized time savings are quite impressive; Michael estimated
the savings to add up to nearly 40 minutes for each developer in a normal working day.

Though the individual advantages are obvious, I was critical about the underlying process of feature- (respectively ticket-) branching.
Nearly everything in professional software development
[depends on the context](http://andreas-simon.blogspot.com/2011/02/photographic-testing-lessons-learned.html) of your team / project.
So this process might just be the right one for Michael's team.
My specific opinion about feature branches is based on the articles of
[Martin Fowler](http://www.martinfowler.com) on
[feature branches](http://martinfowler.com/bliki/FeatureBranch.html),
[feature toggles](http://martinfowler.com/bliki/FeatureToggle.html), and
[semantic merge conflicts](http://martinfowler.com/bliki/SemanticConflict.html).

The basic problem about feature branches is the deferred merging. It is a long known fact that the
cost of bug fixing correlates with the length of the time span between bug creation and bug detection.
By creating a new branch for each new feature / ticket, you avoid early, continuous integration.
When you have to integrate later on---before pushing and making the pull request---your knowledge is
not as fresh as at the time writing the new code. Thus, it might be harder to fix merge
conflicts---be it obvious conflicts detected by your version control system, or hidden
[semantic conflicts](http://martinfowler.com/bliki/SemanticConflict.html) with the code of your team
mates. That is why I tend to prefer continuous integration in the trunk / master of your project.

If everybody commits to the same branch, you will be faced with another problem: what do you do with
not-yet-finished features that you don't want to release yet? Martin Fowler advices
the use of [feature toggles](http://martinfowler.com/bliki/FeatureToggle.html), a.k.a feature flags.
The idea is basically this: you create a single point in your code where you manage
the activation of your various features. Since features affect the GUI mainly, you insert
conditional statements in your view code that displays the respective elements based
on the activation of the feature.

I want to give a small, practical example: The [Envie gem](http://rubygems.org/gems/envie) makes it
very easy to use feature toggles within Ruby on Rails applications. You define your environments
(e.g. development and test) inside `environment.rb`:

    development = Envie.development.with(:blog).with(:profile)
    test        = development.derive(:test)

That means, in the development environment, you activate the 'blog' and 'profile' features. The test
environment enables the same features as the development environment. In any
other environment, none of the features is active. To check whether a specific feature is enabled,
just use the `feature()` method with a block of view code:

    <% feature(:blog) do %>
      <h2>My Blog</h2>
    <% end %>

By default, a feature is inactive. You have to enable a feature explicitly. When you rolled out the
feature and detect some bug in production, it is easy to withdraw it by
switching off the feature toggle. When the feature is in production successfully for a while, you
should delete the feature toggle from your code; this prevents the pollution of your code with
feature toggles.

At the time of presenting it, the new tool was in production for one week at BleacherReport.
I am looking forward to Michael's long-term experiences.
