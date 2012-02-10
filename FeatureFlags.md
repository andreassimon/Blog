On Feature Flags
================

During the last MonsterOnRails meetup we hit the topic auf feature management in larger development teams. Michael Schäfermeier presented
a new process employed at http://www.bleacherreport.com. They make extensive use of GitHub's forking and pull request mechanisms.
To ease the correct handling of Git and Lighthouse, Winton Welsh developed a wrapper for Git, called [gitcycle][https://github.com/winton/gitcycle].

The realized time savings are quite impressive; in a normal working day, Michael estimated the savings to add up to nearly 40 minutes.

Though the individual advantages are obvious, I was critical about their actual process using feature branching.
I tend to sound a little black and white at times. I want to make clear that I do not believe in general best practices; nearly everything in professional
software development [depends on the context][http://andreas-simon.blogspot.com/2011/02/photographic-testing-lessons-learned.html] of your team / project.
My opinion about feature branches is based on the articles of [Martin Fowler][http://www.martinfowler.com] on [feature branches][http://martinfowler.com/bliki/FeatureBranch.html],
[feature toggles][http://martinfowler.com/bliki/FeatureToggle.html], and [semantic conflicts][http://martinfowler.com/bliki/SemanticConflict.html].

The basic problem about feature branches is the deferred merging. It is a long known fact that the cost of bug fixing correlates to the time between bug creation and bug detection.
By creating a new branch for each new feature / ticket, you circumvent continuous integration. When you have to integrate later, your knowledge is not as fresh as at the time writing the new code.
Thus, it might be harder to fix merge conflicts---be it obvious conflicts detected by your version control system, or hidden
[semantic conflicts][http://martinfowler.com/bliki/SemanticConflict.html] with the code of your team mates. That is why I would prefer continuous integration in the trunk / master of your project.

When everybody works an the same branch, you are faced with another problem: what do you do about not-yet-finished features that you don't want to release yet? Martin Fowler advices the use of [feature toggles][http://martinfowler.com/bliki/FeatureToggle.html], a.k.a feature flags. The idea is basically this: you create a single point in your code where you manage the activation of your various features.

I am really looking forward to Michael's future experiences. Possibly---and I hope so for Michael's team---I am dead wrong and their ideas work out as intended.






