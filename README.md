# Bulk Downloader for Reddit
This program downloads imgur, gfycat and direct image and video links of saved posts from a reddit account. It is written in Python 3.
  
**PLEASE** post any issue you had with the script to [Issues](https://github.com/aliparlakci/bulk-downloader-for-reddit/issues) tab. Since I don't have any testers or contributers I need your feedback.

## Table of Contents

- [What it can do?](#what-it-can-do)
- [Requirements](#requirements)
- [Setting up the script](#setting-up-the-script)
  - [Creating an imgur app](#creating-an-imgur-app)
- [Program Modes](#program-modes)
- [Running the script](#running-the-script)
  - [Using the command line arguments](#using-the-command-line-arguments)
- [Examples](#examples)
- [FAQ](#faq)
- [Changelog](#changelog)

## What it can do?
### It...
- can get posts from: frontpage, subreddits, multireddits, redditor's submissions, upvoted and saved posts; search results or just plain reddit links
- sorts posts by hot, top, new and so on
- downloads imgur albums, gfycat links, [self posts](#i-cant-open-the-self-posts) and any link to a direct image
- skips the existing ones
- puts post titles to file's name
- puts every post to its subreddit's folder
- saves a reusable copy of posts' details that are found so that they can be re-downloaded again
- logs failed ones in a file to so that you can try to download them later
- can be run with double-clicking on Windows (but I don't recommend it)

## Requirements
- Python >3.6

You can install Python 3 here: [https://www.python.org/downloads/](https://www.python.org/downloads/)  
  
You have to check "**Add Python 3 to PATH**" option when installing in order it to run correctly.
  
## Setting up the script
Because this is not a commercial app, you need to create an imgur developer app in order API to work.

### Creating an imgur app
* Go to https://api.imgur.com/oauth2/addclient
* Enter a name into the **Application Name** field.
* Pick **Anonymous usage without user authorization** as an **Authorization type**\*
* Enter your email into the Email field.
* Correct CHAPTCHA
* Click **submit** button  
  
It should redirect to a page which shows your **imgur_client_id** and **imgur_client_secret**
  
\*Select **OAuth 2 authorization without a callback URL** first then select **Anonymous usage without user authorization** if it says *Authorization callback URL: required*

## Program Modes
- **saved mode**
  - Gets posts from given user's saved posts.
- **submitted mode**
  - Gets posts from given user's submitted posts.
- **upvoted mode**
  - Gets posts from given user's upvoted posts.
- **subreddit mode**
  - Gets posts from given subreddit or subreddits that is sorted by given type and limited by given number.
- **multireddit mode**
  - Gets posts from given user's given multireddit that is sorted by given type and limited by given number.  
- **link mode**
  - Gets posts from given reddit link.  
  - You may customize the behaviour with `--sort`, `--time`, `--limit`.
  - This mode is only accessible via command-line arguments. See **[`python script.py --help`](#using-the-command-line-arguments)**
- **log read mode**
  - Takes a log file which created by itself (json files), reads posts and tries downloading them again.
  - Running log read mode for FAILED.json file once after the download is complete is **HIGHLY** recommended as unexpected problems may occur.

## Running the script
Letting more than one instance of the script run is **not** suggested as it interferes with IMGUR Request Rate.  
  
### Using the command line arguments
If no arguments are passed program will prompt you for arguments below which means you may start up the script with double-clicking on it (at least on Windows for sure).
  
Open up the [terminal](https://www.reddit.com/r/NSFW411/comments/8vtnl8/meta_i_made_reddit_downloader_that_can_download/e1rnbnl) and navigate to where script.py is. If you are unfamiliar with changing directories in terminal see Change Directories in [this article](https://lifehacker.com/5633909/who-needs-a-mouse-learn-to-use-the-command-line-for-almost-anything).
  
Run the script.py file from terminal with command-line arguments. Here is the help page:  
  
Use `.\` for current directory and `..\` for upper directory when using short directories, otherwise it might act weird.

```console
$ python script.py --help
usage: script.py [-h] [--link link] [--saved] [--submitted] [--upvoted]
                 [--log LOG FILE] [--subreddit SUBREDDIT [SUBREDDIT ...]]
                 [--multireddit MULTIREDDIT] [--user redditor]
                 [--search query] [--sort SORT TYPE] [--limit Limit]
                 [--time TIME_LIMIT] [--NoDownload]
                 DIRECTORY

This program downloads media from reddit posts

positional arguments:
  DIRECTORY             Specifies the directory where posts will be downloaded
                        to

optional arguments:
  -h, --help            show this help message and exit
  --link link, -l link  Get posts from link
  --saved               Triggers saved mode
  --submitted           Gets posts of --user
  --upvoted             Gets upvoted posts of --user
  --log LOG FILE        Triggers log read mode and takes a log file
  --subreddit SUBREDDIT [SUBREDDIT ...]
                        Triggers subreddit mode and takes subreddit's name
                        without r/. use "frontpage" for frontpage
  --multireddit MULTIREDDIT
                        Triggers multireddit mode and takes multireddit's name
                        without m/
  --user redditor       reddit username if needed. use "me" for current user
  --search query        Searches for given query in given subreddits
  --sort SORT TYPE      Either hot, top, new, controversial, rising or
                        relevance default: hot
  --limit Limit         default: unlimited
  --time TIME_LIMIT     Either hour, day, week, month, year or all. default:
                        all
  --NoDownload          Just gets the posts and store them in a file for
                        downloading later
```  

## Examples

- **Don't include `python script.py` part if you start the script by double-clicking**
- **Use `python3` instead of `python` if you are using *MacOS* or *Linux***  

```console
python script.py .\\NEW_FOLDER --sort new --time all --limit 10 --link "https://www.reddit.com/r/gifs/search?q=dogs&restrict_sr=on&type=link&sort=new&t=month"
```

```console
python script.py .\\NEW_FOLDER --link "https://www.reddit.com/r/learnprogramming/comments/7mjw12/"
```

```console
python script.py .\\NEW_FOLDER --search cats --sort new --time all --subreddit gifs pics --NoDownload
```

```console
python script.py .\\NEW_FOLDER --user [USER_NAME] --submitted --limit 10
```

```console
python script.py .\\NEW_FOLDER --multireddit good_subs --user [USER_NAME] --sort top --time week --limit 250
```

```console
python script.py .\\NEW_FOLDER\\ANOTHER_FOLDER --saved --limit 1000
```

```console
python script.py C:\\NEW_FOLDER\\ANOTHER_FOLDER --log UNNAMED_FOLDER\\FAILED.json
```

## FAQ
### I can't startup the script no matter what.
- Try these:
  - **`python`**
  - **`python3`**
  - **`python3.7`**
  - **`python3.6`**
  - **`py -3`**  
    
Python have real issues about naming their program

### I can't open the self post files.
- Self posts are held at reddit as styled with markdown. So, the script downloads them as they are in order not to lose their stylings. However, there is a great Chrome extension [here](https://chrome.google.com/webstore/detail/markdown-viewer/ckkdlimhmcjmikdlpkmbgfkaikojcbjk) for viewing Markdown files with its styling. Install it and open the files with Chrome.

## Changelog
### [11/07/2018]()
- Improvements on UX and UI
- Added logging errors to CONSOLE_LOG.txt
- Using current directory if directory has not been given yet.
### [10/07/2018](https://github.com/aliparlakci/bulk-downloader-for-reddit/tree/ffe3839aee6dc1a552d95154d817aefc2b66af81)
- Added support for *self* post
- Now getting posts is quicker
