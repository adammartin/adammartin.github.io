---
layout: post
title:  "Discipline in development ... Oh my!"
date:   2014-03-02 09:46:00
categories: Craftmanship
---

I enjoy discipline in my craft.  I am an avid believer in the fail fast mentality.  A smart developer knows to use his compiler (in compiled languages) to identify fail points and correct items prior to execution. For those of us who have adopted the virtues extoled by [eXtreme Programming](http://www.extremeprogramming.org/) we have hardened that with a rigor of unit testing, refactoring, etc.

As my experience has grown and I’ve seen more projects succeed and fail, budgets managed or squandered, I’ve greatly came to appreciate when quality can be taken off the platter for management worries.  As Uncle Bob is oft to say, [“The only way to go fast, is to go well.”](http://blog.8thlight.com/uncle-bob/2013/03/05/TheStartUpTrap.html)

I’ve taken this discipline to heart and have wrapped this into a series of preferences I enjoy to have established as part of every project.  Many of the concepts exist as part of other practices, continuous integration and XP for example.  I haven’t seen a short list expressed in the past this way, so I share with you my standard.

Continuous Integration
----------------------

First and foremost for any project of importance, I strongly believe a CI system must be in place.  There is a plethora of blogs out there on CI so my goal is not to go into depth on how to implement but simply state you should have:

1.	A source control system (I recommend [git](http://git-scm.com/) or [mercurial](http://mercurial.selenic.com/)).
2.	A Continuous Integration server (use [Jenkins](http://jenkins-ci.org/) there is nothing else equal).
3.	A big visible way to view the state of the build.

There are many other pieces and parts we can detail out, but these three foundational components are what I leverage.

Craftsmanship Contract
----------------------

There are discussions at nausea on the topic of team norms.  Craftsmanship Contracts are akin to team norms but instead focus on the standards the team agrees there coding practices should be held to.  They are living documents and the standards apply to every card (there are exceptions but those should be discussed by the team).  

These standards form an agreement between the team members on how they promise to protect leadership from quality concerns.  It may be a complex or simple document and it only matters that the team truly holds themselves accountable (accountability includes the team makes it big and visible).

Often these contracts will express the norms around testing, test coverage, static analysis, coding standards, fail fast mechanisms, peer reviews, etc.  All team members ought adhere to these rules.  Senior architects or developers are not exceptions.  They are members of the team.  No member is so special or so amazing that their code is allowed to diverge from the standards.

Why? Because a group of good developers, acting as a cohesive group, with high quality standards, will always out perform a group of brilliant hackers over the long haul.  Refactoring, changing business requirements, technical discovery, individual career changes, etc. all but guarantees that a cohesive group who can change code with no fear will excel for a significantly longer time frame then those who do not operate with said discipline.

Finally print this contract out with every iterative change it goes through, and get every team member to sign it.  It should be big and visible on a wall. When pressure to ‘hurry’ or to ‘just break the rules this one time’ occurs point at your big and visible and as a team say “NO”.  If upper management still wants to push, ask them if they would request the electrician to “use cheap wiring in their house and please hurry the wiring in the children’s bedroom with no insulation?”  That is what they are asking.  Violate the project quality agreement even if it may cause the project to burn?  There are cases where upper management has the right to put the project at risk but often quality is thrown to the wind when the project actually should be failed instead (at some point we should discuss failing a project early rather then letting project languish in a state of corruption).

FAIL THE BUILD!
---------------

With a CI system and a standard in place now we begin to fail the build.  Fail fast and fail often!  Failing the build on a CI server is not a scary or terrible thing.  It’s a terrible thing when you introduce defects and failures into production.  On a CI system it’s a learning opportunity for us to see whom we can help to improve their coding abilities. If you can’t tell I believe in applying the [retrospective prime directive](http://www.retrospectives.com/pages/retroPrimeDirective.html) to every day practices.

###Why should we fail a build?

1.	Compilation errors and warnings.  Don’t let anything through.  If you have a warning you don’t want to fail the build for then find a way to remove the warning.  People will not read warnings unless they fail the build so their value should be treated as binary.  In the off case where we truly want it ignored then deduce a way to ignore that one off case rather then making ignorance the norm.
2.	Test failures.  As above don’t let anything through.  No exceptions here, i.e. this counts for all tests on the [testing pyramid](http://watirmelon.com/2011/06/10/yet-another-software-testing-pyramid/).
3.	Unit test “pending” or “disabled”.  Write the test or delete it.  The worst is commented out tests, which can become stale and unable to execute.  We have source control which enables us to restore tests on demand or better yet we can write them fresh when we truly know the requirements.
4.	Insufficient test coverage.  This includes both branch and line coverage which allows us to identify code that is dangerous to adapt and alter later.  I know the warnings around how this can lead to developers ‘gaming’ coverage.  If you find a developer gaming coverage on your project I have a different answer … remove them.  It’s another fast feedback mechanism.  Fundamentally there are 2 types of developers who miss coverage, those who do it due to lack of skill, and those who do it due to a lack of belief in testing.  For the former we find them fast and create a safe environment to grow them.  For the later we remove them so they don’t poison our quality standards.
5.	Excessive Test Execution Time.  Long running tests are the bane of a craftsman.  They inherently violate fail fast.  If you want developers to eventually disable tests then let long running tests rot your code base.  Set a max execution time per test and fail them.
6.	Static analysis.  If you have code standards (all data structures should be immutable, no method should take more then 3 arguments, no method should be more then 10 lines, no more then 3 public methods per class, etc.) then you should find ways to enforce them via static analysis.   Just fail the build.  Virtually all static analysis tools have a way to ignore one offs so my fundamental belief is to crank them as tight as possible and only loosen the standard when we are getting excessive exceptions (magic number 3 should start the discussion).

When do we build or check for failure?  On every commit!  On my current project we execute these checks on every single pull request.

Conclusion
----------

Wow that is a lot of rules and it may seem excessive to some.  My experience having split the line between development and management is that well defined quality and well-defined execution rate is invaluable to a project with any serious scope.  If you are throwing up a blog site with static pages then likely there is no value to this level of discipline but if your business is planning to invest $300k to $300 million this discipline gives them the comfort that they can gauge risk and viability.  Why would you rob them of that?  Software development is not a game; it’s a craft, a craft of discipline.  Discipline need not rob creativity or freedom, indeed as a fan of [Leon Gersing](https://github.com/leongersing) (aka Ruby Buddha), I believe in keeping coding fun and dynamic.  However, I believe that discipline frees creative geniuses to experiment with a safety net.  The have an ability to take technical risks with knowledge that they can fall back to a safe state or that system failure will be caught.
