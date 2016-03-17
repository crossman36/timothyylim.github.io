### uploading H5P packages with OSX

This article assumes that you've completed the ['hello world' H5P tutorial](https://h5p.org/tutorial-greeting-card) until the stage where you have to upload a package.

When uploading h5p packages to drupal with osx, you may encouter the following errors:

```
Could not find library.json file with valid json format for library greeting
A valid content folder is missing
A valid main h5p.json file is missing
```

As mentioned in the comments on the tutorial page, these errors are caused by zipping the project folder as opposed to all the files within it.

We can zip all the files within the project file using the terminal (we will use the greeter tutorial as an example):

Navigate into the project

```
$ cd greeting
```

Let's have a look inside

```
$ ls

H5P.GreetingCard	content			h5p.json
```

zip the all the files in greeting to a file called greeter.h5p

```
$ zip -r greeter.h5p *
```

Depending on whether the files in greeter have been accessed using finder, this may be successful or the following erros may occur:

```
File ".DS_Store" not allowed. Only files with the following extensions are allowed: json png jpg jpeg gif bmp tif tiff svg eot ttf woff otf webm mp4 ogg mp3 txt pdf rtf doc docx xls xlsx ppt pptx odt ods odp xml csv diff patch swf md textile.

The uploaded file was not a valid H5P package
```
This error is caused by uploading DS_Store files which are created by Finder whenever you open a file.

Remove the corrupted zip file if you haven't already

```
$ rm -rf greeting.h5p
``` 

Recursively delete the .DS_Store files, don't open the directory in Finder after this step

```
$ find . -name '.DS_Store' -delete
```

Create the zip file again

```
$ zip -r greeter.h5p *
```

that should be it. Check out the official [H5P forum](https://h5p.org/forum) if you have any other problems.
