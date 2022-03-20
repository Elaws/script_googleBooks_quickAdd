# Books script for Obsidian's Quickadd plugin

## Demo
![googleBooksDemo](https://user-images.githubusercontent.com/52013479/151622323-294cca54-f661-4ff3-95e6-4fe7a7e7ea9b.gif)

If this script helped you and you wish to contribute :)

<a href="https://www.buymeacoffee.com/elawsdev4" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

## Description

This script allows you to easily insert a book note into your Obsidian vault using [Quickadd plugin](https://github.com/chhoumann/quickadd) by @chhoumann. **Now also works on Mobile (make sure you use latest QuickAdd) !**
Possible to query book using :
- a book title or ISBN (10 or 13). 
- (optional) author name

It's also possible to query book using author name only (just skip book title prompt).

The `(i)` prefix in search suggestions indicates that an image is available for this book.

We use Google Books API to get the book information.

An API KEY for Google Books is needed to use this script : it can be obtained [here](https://console.developers.google.com/apis/credentials). Steps to obtain this key are detailed below (see [How to obtain Google Book's API key](#how-to-obtain-google-books-api-key)).

## Disclaimer

The script and this tutorial are based on [Macro_MovieAndSeriesScript.md](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_MovieAndSeriesScript.md) by @chhoumann.

**Please never run a script that you don't understand. I cannot and will not be liable for any damage caused by the use of this script. Regularly make a backup of your Obsidian's vault !**

## How to obtain Google Book's API key

1. Visit [this website](https://console.developers.google.com/apis/credentials).
2. Login using your Google account.
3. When prompted, accept the terms of use :

![0](https://user-images.githubusercontent.com/52013479/151619294-85229684-821d-4d50-b99d-c4b9aba70b8f.png)

4. Click on "Create a project" :

![1](https://user-images.githubusercontent.com/52013479/151619359-38879068-595b-4c10-a3e6-ffc575755f1f.png)

5. Enter a project name :

![2](https://user-images.githubusercontent.com/52013479/151619395-8835e1b5-218d-4763-89a4-7ff89ed13fcb.png)

6. Back on the credentials page, click on "Create credentials" :

![3](https://user-images.githubusercontent.com/52013479/151619475-89154b57-bf7f-435b-ba54-e46d24547c74.png)

7. In the menu that appeared, select "API Key" :

![4](https://user-images.githubusercontent.com/52013479/151619531-7555f6cf-16b7-4af8-8c79-4c252b614af8.png)

8. You should see your API key. Close the window :

![5](https://user-images.githubusercontent.com/52013479/151619579-e4691a4b-89ca-4420-ac4e-9dcd465bae40.png)

9. Here is your API key :

![key](https://user-images.githubusercontent.com/52013479/151620113-763477bf-1d4d-4888-af60-932d4c6635d2.png)

10. We must now enable Google Books API for this key. Back on the credentials page, click on "APIs and services" :

![6](https://user-images.githubusercontent.com/52013479/151619643-762730ff-ee6c-4053-8882-f4c175d0310b.png)

11. Click on "Enable APIs and services" :

![7](https://user-images.githubusercontent.com/52013479/151619722-1e7c04e3-be23-4d31-bde1-b97d88b6590a.png)

12. Enter "Google books" in the search bar that appeared :

![8](https://user-images.githubusercontent.com/52013479/151619784-626bb529-190f-49a0-9ad8-095a702f3f99.png)

13. Select "Books API" :

![9](https://user-images.githubusercontent.com/52013479/151619814-ae050972-ae34-4eec-8257-f982d6b7485c.png)

14. Enable Google Books API by clicking on "Enable" :

![10](https://user-images.githubusercontent.com/52013479/151619886-f5774148-6489-45c7-be64-47211e45f704.png)


## Installation
![googleBooksInstall](https://user-images.githubusercontent.com/52013479/151622434-7ce2ebbc-847f-48cb-b867-d103238ec5bf.gif)

0. Make sure you use latest Quickadd version (at least 0.5.1) !
1. Save the [script](https://github.com/Elaws/script_googleBooks_quickAdd/releases) to your vault somewhere. Make sure it is saved as a JavaScript file, meaning that it has the `.js` at the end.
2. Create a new template in your designated templates folder. Example template is provided below.
3. Open the Macro Manager by opening the QuickAdd plugin settings and clicking `Manage Macros`.
4. Create a new Macro - you decide what to name it.
5. Add the user script to the command list.
6. Add a new Template step to the macro. This will be what creates the note in your vault. Settings are as follows:
    1. Set the template path to the template you created.
    2. Enable File Name Format and use `{{VALUE:fileName}}` as the file name format. You can specify this however you like. The `fileName` value is the name of book without illegal file name characters.
    3. The remaining settings are for you to specify depending on your needs.
7. Click on the cog icon to the right of the script step to configure the script settings. This should allow you to enter the API key you got from Google Books API. **Make sure no spaces are inserted before or after the key !**
8. Go back out to your QuickAdd main menu and add a new Macro choice. Again, you decide the name. This is what activates the macro.
9. Attach the Macro to the Macro Choice you just created. Do so by clicking the cog ⚙ icon and selecting it.

You can now use the macro to create notes with book information in your vault !

### Example template

Please also find a definition of the variables used in this template below (see : [Template variable definitions](#template-variable-definitions)).

```markdown
# {{VALUE:title}}

Title:: {{VALUE:title}}
linking:: [[% Novels]] 
Tags:: #📥/📚/{{VALUE:tag}}
Author:: {{VALUE:authors}}
Publish date:: {{VALUE:release}}
Cover:: {{VALUE:thumbnail}}
ISBN10:: {{VALUE:isbn10}}
ISBN13:: {{VALUE:isbn13}}
URL:: [Goodreads]({{VALUE:goodreadsURL}})
Genre:: {{VALUE:genre}}
PageCount:: {{VALUE:pageCount}}
AverageRating:: {{VALUE:avRating}}
Rating:: {{VALUE:rating}}
Maturity:: {{VALUE:mature}}
Read:: {{VALUE:read}}
Recommender:: {{VALUE:recommender}}
Date:: {{DATE}}
Comment:: {{VALUE:comment}}
BookDescription:: {{VALUE: bookDesc}}

```

## Dataview rendering

Here is the dataview query used in the demo (replace `PATH` by your videogames notes path) :

```dataview
TABLE WITHOUT ID

("[[" + file.name + "|" + Title + "]]") AS Title,
Author,
publish-date AS "Publish date",
("![coverImg|100](" + Cover + ")") as Cover,
rating AS "Rating",
AverageRating AS "Average Rating",
Maturity AS "Maturity Rating",
PageCount AS "Page Count",
BookDescription AS "Book Description",
Genre,
Recommender,
Comment,
Date,
URL

FROM "PATH"

SORT Title
```

The banner at the top of the document is rendered using [Obsidian-banners](https://github.com/noatpad/obsidian-banners) plugin.

## Template variable definitions

Please find here a definition of the possible variables to be used in your template. Simply write `{{VALUE:name}}` in your template, and replace `name` by the desired book data, including :

`fileName` : Title of the book without illegal characters. Possibly used in template configuration to name your file.

`title` : The title of the book.

`tag` : A colored square that is red if unread, orange if read.  

`authors` : Book's author.

`release` : The year this edition of the book was published.

`thumbnail` : A book cover, whenever possible.

`isbn10` : The ISBN 10 of the book.

`isbn13` : The ISBN 13 of the book.

`goodreadsURL` : An URL that uses the ISBN to request Goodreads book page. This may fail if ISBN returned by Google is not in the database of Goodreads.

`rating` : Your book rating, /10.

`avRating` : Average rating from all ratings in API.

`genre` : The reported genre of the book.

`pageCount` : Total number of pages in this book.

`mature` : Is this book rated mature or not?

`bookDesc` : What is the blurb of the book?

`read` : If you read the book, this equals 1, otherwise 0 (this helps to filter dataview query).

`recommender` : The person (or organization, etc...) that recommended the book to you.

`comment` : A short personal comment on the book.
