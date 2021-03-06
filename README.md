# Building an AI Poker Tournament: Quick Collaboration Using Bluemix DevOps Open Toolchain
---

## Introduction

Welcome! In this quick lab we'll be using the [Bluemix Continuous Delivery](https://www.ibm.com/blogs/bluemix/2016/11/bluemix-continuous-delivery-is-now-live/) feature of Bluemix to run an automated poker tournament among robot players. We will create a GitHub integration in our toolchain to copy the code in this repository and flow it to a Delivery Pipeline integration to run the tournament.

Bolder participants with knowledge of JavaScript and poker mechanics will also be able to create their own AI players and contribute them back to this repository, competing against the other attendees of this session.

A complementary leaderboard application will keep track of the current standings of the bots in this repository. You can view the results of past tournaments at this link: [ic17-otc-poker-leaderboard.mybluemix.net](https://ic17-otc-poker-leaderboard.mybluemix.net)

Any additions to this repository (through pull requests) will automatically trigger a run of a set of tournaments, which will update the leaderboard automatically. The last 5 sets of tournaments, with the timestamp, players, and chip totals of each AI will be displayed.

The [code for this leaderboard](https://github.com/melickm/OpenToolchainPokerLeaderboard) is also deployed to Bluemix using a toolchain. If you want to learn more about the infrastructure surrounding this lab, let me know and I can give you a quick demo.

Let's begin running your own tournament. As with any other lab, please don't hesitate to ask questions if you get stuck. Enjoy!

*The code for this lab was built on the [JsPoker](https://github.com/mdp/JsPoker) project by Mark Percival. Check it out if this lab interests you.*

----
### What is a toolchain?

A toolchain is connected set of tools that can be adapted to suit the needs of a software development team. Different teams may have entirely different toolchains, as they are unique to the different development practices or culture of the team. The idea is championed by the [Bluemix Garage Method](https://www.ibm.com/devops/method) as a DevOps practice for delivering code in a more effective way.

This toolchain concept has been implemented as a Bluemix feature to allow users to collect and integrate a set of tools from a common tool catalogue with minimal configuration. This allows development teams to try out new tools easily and to adapt their tools to each individual project, discovering and switching tools as they see fit.

Templates can also be easily created to share toolchain configurations and settings with others, allowing teams to setup a full development environment in just a few seconds.

In our lab, we will utilize a handful of integrations to run our code quickly. Feel free to diverge from the lab and experiment with adding different tools as we go along. For instance, adding a _Slack_ integration will allow the _Delivery Pipeline_ to post a message to a Slack channel whenever a build is run.

[More information on Open Toolchain](https://www.ibm.com/devops/method/category/tools)

----

### Prerequisite Accounts

You will need to sign up for a [Bluemix](https://interconnectlabs.mybluemix.net/) account for this lab, if you don't already own one.

For those creating a new Bluemix account, you will also need to create an _organization_ and a _space_ in your account after logging in.


You will also need a free [GitHub](https://github.com/) account. Review the [terms of service](https://help.github.com/articles/github-terms-of-service/), and, if you agree with the terms, create an account. GitHub is a service for collaboration in software development. We will use GitHub in this lab to host our source code in a repository.

--------

### Creating a Toolchain and running the tournament

1. Go to [Bluemix](https://interconnectlabs.mybluemix.net/) to begin the lab. Here you can either open a new Bluemix account (it's free!) or choose to use an existing account.

1. Next, navigate to the IBM DevOps Services page in Bluemix at [https://bluemix.net/devops](https://bluemix.net/devops).

1. You should now be on the Toolchains page. Click on `Create a toolchain`.

1. Select the `Build your own toolchain` template.

1. Choose a name and click `Create` to finish the creation process.

1. The toolchain overview page will open. From here, we'll want to add some integrations to the toolchain. Click the `Add a Tool` button.

1. Select `GitHub`. You may need to **Authorize** GitHub if this is your first time using it in a Toolchain. This integration will link a GitHub repository to the toolchain, which will allow users to flow the source code to other integrations.

1. After authorizing, choose `Fork` as the Repository Type and enter the URL of this repository as the Source Repository URL https://github.com/melickm/OpenToolchainPoker. A fork will create a new repository in your GitHub account with the identical source code and history of this parent directory. Click `Create Integration`.

1. A GitHub repository should now be displayed in your toolchain. The source code for this lab is now linked to your toolchain. Click on the `Add a Tool` button again to add another integration to use the source code.

1. Select the `Delivery Pipeline`. Enter a name for your pipeline and click `Create Integration`.

1. The _Delivery Pipeline_ service is used to run and deploy code to Bluemix with a great deal of configurability. We will be using this service to run the source code from the GitHub repository to simulate poker tournaments. Click into the new Pipeline tile on your toolchain page.

1. From this screen, we will start constructing pipeline stages used for defining what to do when new code is delivered. Click on `Add Stage` to create a new Pipeline stage. You can give the stage a suitable tournament-sounding name.

1. In the `Input` tab, verify that the **Input Type** is set to `SCM Repository` and that the **Stage Trigger** is set to `Run jobs whenever a change is pushed to Git`. Afterwards, click the `Jobs` tab on the top bar.

1.  Click `Add Job` and create a new `Build` job.

1. Set **Builder Type** of the build job to be `npm`, as our source code is written in Node.js.

1. In the `Build Shell Command` text box, after `npm install`, make a new line and type in `node play`. This will allow the pipeline to run our simulation script when we run this stage.

1. Click the `Save` button at the bottom of the page to save the stage.

1. In the newly created stage, click on the `Build` job in the middle of the tile.

1. Click `Run` at the top and an automated poker simulation will run in the console. You can use the down arrow at the bottom right of the screen to quickly navigate to the end of the tournament.

The tournament will list out the action that each bot took, at each stage of the game. The simulation is set to run for a limit of 200 hands, but will finish early if there is a winner. You can study the actions of each bot and the success of it's strategy as the game progresses, but the specific algorithms that denote the strategy of each bot will be explored in the latter part of the lab.

Feel free to re-run the stage a few times to see the results of different tournaments. You may notice a high variability of winners because the current bots in the tournament use very basic strategies. More effective strategies may result in more consistent winners.

The latter parts of the lab are encouraged, but optional. They deal with creating your own bot, which will require some knowledge of JavaScript and poker. Feel free to also explore the toolchain features of Bluemix or the many different tool integrations available today.

We hope you enjoyed experimenting with Open Toolchains and running poker simulations with Bluemix!

## Before you go!
1. Don't forget to log out of both [GitHub](https://github.com) and [Bluemix](https://bluemix.net).

1. [Scan this QR code](https://chart.googleapis.com/chart?chs=500x500&cht=qr&chl=QR235) and **go claim a T-Shirt** from the info desk!

Please let us know if you have any questions, concerns, or feedback for our product. Any feedback for the lab specifically would also be greatly appreciated.

_If you want to learn more about the poker simulation framework, check out the [JsPoker](https://github.com/mdp/JsPoker) repository._

-----
## Creating your own bot
----
### Create a test stage

In production environments of software development teams, test stages are often used in the _Delivery Pipeline_ to flow new changes through automated tests before they are deployed to different environments.

We will first create a test stage in your toolchain to run a tournament with minimal output, as a method to test your bot quickly. This is the test harness to ensure that your bot is behaving as expected, before running larger simulations with it.

Repeat the steps for adding a stage until saving the newly created stage from the first part of the lab (steps 12-17), but instead of entering `node play` in the `Build Shell Command` text box, use `node test/challenger_test.js` for the run command instead. Save the stage and run it to quickly see the success of the `challengerBot`. Note that the `Input` tab should have `Run jobs when the previous stage is completed` selected.

### Modify ChallengerBot

To experiment with a new player, you will need to edit the `players/challengerBot.js` file of the repository.

Create an `Eclipse Orion Web IDE` integration in the toolchain. The Web IDE creates an instance of the Orion Web Editor, which will allow us to make changes to the source code from inside the browser. Click into the integration to navigate to the root of the repository.

Expand the `players` folder and open the `challengerBot.js` file. You should see an *update* function. The logic of your bot will reside in this function, although you can create helper methods and classes outside of the function. All the code must stay in this file and there can be no references to external modules.

The *update* function will direct the behaviour of your bot. It will be called multiple times within a single round of the tournament and the **game** parameter of the function holds all the information about the game that will be visible to your bot at that time. You can find examples of some game states in the `players/gameStates` folder.

To put it simply, the *update* function just needs to return an integer. If the value is equal to the current call amount (`game.betting.call`), it is considered a *call*. Any amount lower is a *fold*, any amount higher or equal to `game.betting.raise` is a *raise*.

The other players of the tournament can be found in the players folder, their logic is pretty simple so you can learn from their source code easily. More complex algorithms can be found in the `players/veterans` folder, for advanced techniques.

More information about making bots can also be found in the [JsPoker](https://github.com/mdp/JsPoker) readme.

Feel free to also wave down one of the lab moderators to discuss potential algorithms.

### Committing changes

After making your changes to `challengerBot.js`, click the `Git` icon on the left bar of the Web IDE.

Once it finishes loading, the left side of the screen should display all the files that have been changed. Enter a commit message for your change and click the `Commit` button on the top right.

A commit should show up in the `Outgoing` dropdown on the left side of the screen. Click the `Push` button to commit your changes to the repository.

The _Delivery Pipeline_ was configured to run the test stage and run a tournament whenever new changes are pushed to the repository. Navigate back to it on the toolchain to view the results of the latest simulation (with your changes).

### Contribute your bot to the repository

When you are comfortable with the behaviour of your bot, you can contribute it back to the repository for other attendees of the lab to run simulations against.

- Take the logic you've put in _challengerBot_ and create a new file in the `players` folder.
- Give the bot a suitable filename and fill in the name for the bot in the `info` object. Feel free to also leave your email and btcWallet.
- Revert any changes you made to `challengerBot.js`. You can do this by copying and pasting from the challengerTemplate file.
- Add your new bot to `test/tournament.js` by adding a reference to the module at the top of the file and also adding it into the `table` object.
- Commit your changes to your repository.
- Navigate back to the parent repository https://github.com/melickm/OpenToolchainPoker.
- Go into the `Pull Request` tab and click `New Pull Request`.
- Click `compare across forks` and navigate to your own repository.
- Click `Create Pull Request` and enter a description and optionally a comment.
- Click `Create Pull Request` and flag down a lab moderator to review and merge the code.

After a lab moderator merges the pull request, you should see the live-updated results on [ic17-otc-poker-leaderboard.mybluemix.net](https://ic17-otc-poker-leaderboard.mybluemix.net).

Congratulations on contributing! I wish your bot, the best of luck.
