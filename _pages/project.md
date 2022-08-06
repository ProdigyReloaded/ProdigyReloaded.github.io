---
permalink: /project
author_profile: false
title: "About the Project"
toc: true
---
# Genesis
Prodigy made use of a hierarchical caching mechanism whereby content would first be sought from a cache within the end-users computer, then the regional server, and ultimate the origin server.  These cache retrievals would "warm" the lower layers with popular content, and subject to policies, content may persist on the end-user computer for use in subsequent sessions.

In 2014, Jim Carpenter discovered that the `STAGE.DAT` file to which this content was persisted utilized a FAT-like filesystem, and he developed software to extract these objects and coerce the client into displaying the images contained within.  Benj Edwards writes about Jim's efforts in his article [Where Online Services Go When They Die](https://www.theatlantic.com/technology/archive/2014/07/where-online-services-go-when-they-die/374099/), and the Benj published the imagery that Jim was able to extract from several contributed `STAGE.DAT` files [here](https://www.flickr.com/photos/149332336@N06/albums).

In late 2019, Phil Heller read the article, and given the success in [reviving Quantum Link](https://orrtech.us/qlink/) some years ago, developed an interest in doing the same.

# Cautious Optimism
Like Jim Carpenter, Phil Heller retrieved the Prodigy Patent and the associated application, which included several thousand pages of the source code for the Reception System.  Between the source code and the patent, Phil implemented enough code to convince the client to *try* to connect as detailed in this [blog post](https://www.vintagecomputing.com/index.php/archives/2921/reverse-engineering-prodigy-part-1), but for a while, this was a sticking point, and the project was put on hold.

Some months later the project and made some early progress by simply fuzzing the client with responses of various sizes, ultimately narrowing on a number of login responses that allowed the client to continue.  A greater breakthrough was made when Phil was furnished a number of documents, including the Prodigy "Application Developers Reference Manual".  While not a document of specifications, it included an instructive example of a TBOL debugging session complete with source, and a disassembly of the corresponding binary.  It was this that convinced Phil to redouble efforts to extract virtual machine's instruction set from the patent source and build a disassembler.

A second [blog post](https://www.vintagecomputing.com/index.php/archives/3064/reverse-engineering-prodigy-part-2) was published, detailing the construction of just such a disassembler, and the use of it to further determine the client reqeust and response format for various services.

# Rapid Progress
With a disassembler constructed, Phil continued to build a mock server operating with a similar configuration grammar that Prodigy's own mock server utilized.  More TBOL binaries were disassmbled, more functionality understood, and yet more questions raised.

Given that it seemed likely some part of the service could be revivsed, it was decided to exhibit the project at whatever state it might be in at the Vintage Computer Festival West in August 2022.  As a result, the mock server was entirely rewritten with a real database backend, and then began work to replicate content.

The project is very lucky that some Archive.org contributor rescued and shared the contents of some old floppies in early 2022. Specifically, these files include CREDO (Create and Edit Objects) and GCU (Graphics Creation Utility).

CREDO allows greater inspection of Object files extracted from `STAGE.DAT`, and synthesis of new "objects" for upload to the server and distribution to clients.  GCU provides a NAPLPS editing environment.  These two tools together have made it possible to create and recreate Prodigy content.

The project was named Prodigy Reloaded as the author's nod to the work the Quantum Link enthusiasts did.  As of this writing, the following works within Prodigy Reloaded

- Logon
- Enrollment - Household and User
- Logoff - Normal and Abnormal
- Sending and receiving email
- Retrieving Stock quotes
- Jumpwords and Jumpword Index
- Viewpath (partial)
- Guide Menus
- Highlights Page
- Profile retrieval and update
- The very beginning of MadMaze
- A single static Weather Map

Known issues:

- Email can be neither deleted nor retained
- Some of navigational elements of personal address book and mailing list work, but none of the logic works.
- The user-list does not work for lack of the `CCDAM` driver object.
- "Directory" and "Find" do not work, for lack of the `CCDAM` driver object.
- Quote Track does not work, but there still may be hope that the objects necessary to make this work are available.
- Stock Quotes will fulfill any valid equities quote (via YahooFiannce), but all tickers will resolve to "International Business Machines".
- None of the TCS (Trintex Communications Subsystem) error recovery mechanisms are implemented as of yet, as the intial approach was for the client to connect over reliable TCP sessions.  As such, modem-based connections are susceptible to line noise which often causes the client to timeout or disconnect.o

# Plans
Subsequent to the VCF West show, the author intends to improve the test coverage in the server code, improve documentation, open access to a public server, and publish the repositories for all the tools and the Prodigy server.
