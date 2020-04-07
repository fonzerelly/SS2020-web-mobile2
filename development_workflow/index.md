# Development Workflow

??HORIZONTAL

<img src="development_workflow/images/alice.jpg" width="90%">

??NOTES

Well this band seems to suffer under a wrong team setup. When you look at 
at the song text, you will recognize, that the singer suffers on three different issues.

* He has to fix some code that somebody called alice wrote
* He has no knowledge about it
* The current code fails, which make it worse to handle the issue
* Alice is not availabe, since she is on vacation

So that you do not suffer here and can setup a better Development Process, I would like to point out some asepcts of successfull software teams.

??HORIZONTAL

## Be a Software Development Team

* Get and merge your Software on a daily basis at a central position (e.g. [Github](https://www.github.com)) <!-- .element: class="fragment" -->
* Be sure that the software in the central repository ALWAYS works! <!-- .element: class="fragment" -->
* Ensure that everybody in the team can jump in and knows about the rest of the project <!-- .element: class="fragment" -->

??NOTES
You will probably do that manually. But I want to point out how you do this on the job.

??HORIZONTAL

## Continous Integration Server

* Recognizes changes in the repository <!-- .element: class="fragment" -->
* Downloads changes <!-- .element: class="fragment" -->
* Builds the application <!-- .element: class="fragment" -->
* Runs Static Code Analysis <!-- .element: class="fragment" -->
* Runs Tests <!-- .element: class="fragment" -->
* Informs about Failures <!-- .element: class="fragment" -->
* Uploads Deployables <!-- .element: class="fragment" -->

??NOTES
Build, Static Code Analysis and Tests are so called Quality Gates that the
Software has to pass, so that they may be installed in a so called production evironment.

