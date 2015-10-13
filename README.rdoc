YourTradeBase Code Test
=======================

Instructions
------------

This is a very simple rails application that allows users to manage a list of books. The app mainly contains rails auto generated scaffold code, however some code has been added to allow books to be managed via the users show page. This code has not been written very well! We would like you to refactor the code in order to make the code more maintainable and to be written in a style more suited to a well written rails application. There has also been a complaint from some end users that the site is slow to respond occasionally when creating new users. The application has some basic Rspec tests that can be run using the `rspec` command.

Please spend no more than 2 hours on the exercise excluding any time it takes to install the required software such as ruby, gems etc.

We would like you to keep a record of your thought process and actions taken in order to prepare the application and refactor the code, please be as detailed as possible. You should include your explanations as to why the code you have found is badly written and how you think your refactored code will improve the codebase.

We are interested mainly in your thought process through the exercise, don't worry if you don't manage to complete the refactoring in the time allowed, you may add any suggestions for further refactoring you would wish to carry out if you had more time.

Your taske are:

1. Fork this git repository to your own github account then clone it
2. Install the correct ruby version for the project using a ruby version manager of your choice
3. Install the required gems for the project using bundler
5. Setup the applications database
6. Identify code to be refactored
7. Create appropriate commits for your refactored code
8. Create 1 commit with your notes
9. Push the commits to your github repository
10. Provide us with the url of your github fork of the app

Please add your notes below.

Notes
-----

The first thing I noticed was that there was no books controller and the actions for creating and deleting books were included in the users controller. This goes against Rails' convention over configuration. I created a books controller and moved the create_book and destroy_book actions into here to separate concerns and for single responsibilty.

I then added the routes for the book controller actions and removed the logic from the user show page into a partial just to clean up this view. I would normally only do this with code that needed to be reused elsewhere to prevent unnecessary duplication.

I thought that the AdminMailer might be causing the site to respond slowly when creating users. To test this I commented out the action in the users controller and checked the response times in the terminal.

With the AdminMailer:
---
<div align="center">
        <img width="100%" src="/app/assets/images/mailer_test_1.png">
</div>

Without the AdminMailer:
---
<div align="center">
        <img width="100%" src="/app/assets/images/mailer_test_2.png">
</div>

My first thought to solve this was to move the AdminMailer in the user controller down to above the else statement on line 26. My thinking was that Rails being synchronous, the users might be saved and the page rendered before any emails were sent but this didn't seem to be the case as the load times were the same. Unfortunately the two hours were up at this point so I didn't get time to solve this problem. Searching on Google and StackOverflow I found a gem called delayed_job that asynchronously executes longer tasks in the background like sending out emails and this would be one way of solving this problem. Had I more time I would have tried this solution.
