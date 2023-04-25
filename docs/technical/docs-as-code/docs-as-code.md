!!! warning

	work in progress

# Docs as code at Forma.ai

## Benefits of docs as code

We were using Bookstack

## Alternatives

### Docusaurus

Most of our devs work on the backend.

They may not know React

We also don't need a single page app.




# Goals of docs

-   [ ] integrate into codebase and engineering workflow
    -   [ ] for engineering docs
-   [ ] Decrease the fragmentation of the docs
-   [ ] Get feedback from users about the docs
    -   [ ] drift: how in sync are the docs with the code
    -   [ ] did you find what you were looking for?
    -   [ ] 👍 or 👎
    -   [ ] how many views does each page get?
-   [ ] User documentation
    -   [ ] Commissions Analysts
    -   [ ] Sales Reps
    -   [ ] Financial Business partners
    -   [ ] HelpJuice?
-   [ ] Find an alternative to [diagrams.net](http://diagrams.net/) to create diagrams
    -   [ ] inside the markdown?
    -   [ ] excalidraw
    -   [ ] mermaid
    -   [ ] diagrams
    -   [ ] ![](https://t1278589.p.clickup-attachments.com/t1278589/f6259e1a-f1a9-467c-9f09-e5600fa3beb3/image.png)

Documentation quality audit

-   Readability metrics: [https://opensource.com/article/17/10/doc-audits](https://opensource.com/article/17/10/doc-audits)
-   how often is this page updated?

> Documentation as Code (Docs as Code) refers to a philosophy that you should be writing documentation with the same tools as code:

-   Issue Trackers
-   Version Control (Git)
-   Plain Text Markup (Markdown, reStructuredText, Asciidoc)
-   Code Reviews
-   Automated Tests

# Notes on docs tech talks

### Google: How Two Technical Writers Changed Google Engineering Culture

[https://www.youtube.com/watch?v=EnB8GtPuauw](https://www.youtube.com/watch?v=EnB8GtPuauw)

-   g3docs
-   enable engineers to find, create and maintain docs
    -   keep docs in a simple, portable format (Markdown)
    -   next to its associated code
    -   rendering it at a logical URL
-   Why people don't like docs
    -   they don't exist
    -   they're hard to find
    -   they're wrong
-   Why don't people write docs
    -   no time
    -   no incentive
    -   no culture

### Twitter: Creating the culture of documentation

[https://www.youtube.com/watch?v=6y4eQ6gYwdU](https://www.youtube.com/watch?v=6y4eQ6gYwdU)

-   platform (DocBird)
    -   Twitter use Sphinx
    -   implementation of ReadTheDocs
-   Templates
    -   enforce consistency
-   DocDay (community)

### Build Docs like Code (CI for docs)

[https://www.youtube.com/watch?v=wEt_8twQctQ](https://www.youtube.com/watch?v=wEt_8twQctQ)

-   more layers of separation/time between implementation and writing the docs
    -   more inaccurate docs
-   devs dislike the workflow of writing docs
    -   have to switch tools
    -   gets pushed off
-   treat docs like code
    -   docs are stored in git
    -   build doc artifacts (website) automatically
    -   trusted set of reviewers to review docs
    -   docs are tested
        -   content accurate?
        -   do the links work
-   what we gain
    -   promotes collaboration
    -   tracks doc mistakes as bugs
    -   include docs in code review
    -   beautiful, uniform docs
-   versioning docs
-   types of docs
    -   long form docs
        -   user guides
        -   getting started, FAQs
    -   Functional docs
        -   REST APIs
        -   SDKs
        -   man pages
-   mkdocs

### Writing Great docs (by a maintainer of Django docs)

[https://www.youtube.com/watch?v=z3fRu9pkuXE](https://www.youtube.com/watch?v=z3fRu9pkuXE)

-   docs are communication
-   why do people read docs
    -   great docs serve multiple conflicting users
        -   need to document things multiple times
    -   new users
    -   education
    -   support
    -   troubleshooting (annoyed users)
    -   learning internals (devs)
    -   reference
-   who should write docs
    -   great developers (the person who wrote the feature)
        -   Django requires that new patches come with new docs
        -   the person who just wrote the code knows about it the most
        -   write something and get feedback
        -   wiki is where good docs go to die
        -   wiki tells me that you don't really care about your docs
-   what should we document?
    -   ![](https://t1278589.p.clickup-attachments.com/t1278589/c6f74f30-13bf-48d7-8b4b-f7d88be5b703_large.png)
    -   Tutorials
        -   **quick** (new user should feel a win within 30 mins)
        -   **easy** but **not too easy**
        -   show off how the project **feels**
    -   Topic Guides
        -   Conceptual
            -   tutorials are about parroting
            -   topic guides: kick them out of the nest
        -   Comprehensive
            -   tell the **WHY** of the topic
    -   Reference
        -   complete
        -   for experienced users
        -   HOW of the topic
        -   Igor doesn't like auto-generated reference
    -   Troubleshooting
        -   answers to questions asked in anger
        -   FAQ need to be frequently asked
-   which tools should we use?
    -   tools don't matter (but use good ones)
    -   Sphinx
    -   Docco and Pycco

### Spotify: How we're solving internal technical docs

[https://youtu.be/uFGCaZmA6d4](https://youtu.be/uFGCaZmA6d4)

3rd biggest blocker: not being able to find the the info you need

![](https://t1278589.p.clickup-attachments.com/t1278589/dcb95ce2-a4c8-4830-acff-c9c1ff0d4820_large.png)

Challenges (that are solved by docs as code)

![](https://t1278589.p.clickup-attachments.com/t1278589/e8b08c78-1551-4d57-805b-4f135fa23c60_large.png)

Highlight to open a GitHub issue

![](https://t1278589.p.clickup-attachments.com/t1278589/af0c9440-cc60-4922-b1cd-8f64b7c6efdb/image.png)

![](https://t1278589.p.clickup-attachments.com/t1278589/d7a24d11-2447-42a9-9025-21b1ed671998/image.png)

![](https://t1278589.p.clickup-attachments.com/t1278589/a49e5a61-6109-42b4-acd6-c84521fb43df/image.png)

![](https://t1278589.p.clickup-attachments.com/t1278589/bed3210c-29be-4bae-9945-2635b6cb34eb/image.png)

MLP: Minimum lovable product

Vision: Spotifiers using tech docs go from stuck to unstuck in less than 1 minute

[https://backstage.io/blog/2020/09/08/announcing-tech-docs](https://backstage.io/blog/2020/09/08/announcing-tech-docs)
