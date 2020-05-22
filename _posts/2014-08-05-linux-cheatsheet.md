---
layout: post
title:  "Bash command line for Linux - Cheat Sheet"
date:   2014-08-05 13:09:30
categories: linux
comments: true
---

I've found these commands to be very useful but at the same time I can just as easily forget them. Therefore in this post I wanted to add a cheat sheet so I can refer back to it whenever I need to. These are the common ones I used the most

<!--more-->

If there are any you think will also be useful please let me know in the comments below.

---

### Useful commands

The Commands below are the ones I also find useful and need to use more. Learning to master <strong>grep</strong> is definitely one of my priorities.

<table>
  <thead>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>cat</td>
      <td>Concatenate and print (display) the content of files</td>
    </tr>
    <tr>
      <td>chmod</td>
      <td>Change access permissions</td>
    </tr>
    <tr>
      <td>df</td>
      <td>Display free disk space</td>
    </tr>
    <tr>
      <td>echo</td>
      <td>Display message on screen</td>
    </tr>
    <tr>
      <td>env</td>
      <td>Environment variables</td>
    </tr>
    <tr>
      <td>eval</td>
      <td>Evaluate several commands/arguments</td>
    </tr>
    <tr>
      <td>exit</td>
      <td>Exit the shell</td>
    </tr>
    <tr>
      <td>grep</td>
      <td>Search file(s) for lines that match a given pattern</td>
    </tr>
    <tr>
      <td>mkdir</td>
      <td>Create new folder(s)</td>
    </tr>
    <tr>
      <td>passwd</td>
      <td>Modify a user password</td>
    </tr>
    <tr>
      <td>pwd</td>
      <td>Print Working Directory</td>
    </tr>
    <tr>
      <td>ssh</td>
      <td>Secure Shell client (remote login program)</td>
    </tr>
    <tr>
      <td>su</td>
      <td>Substitute user identity</td>
    </tr>
    <tr>
      <td>sudo</td>
      <td>Execute a command as another user</td>
    </tr>
    <tr>
      <td>tail</td>
      <td>Output the last part of file</td>
    </tr>
    <tr>
      <td>tar</td>
      <td>Store, list or extract files in an archive</td>
    </tr>
  </tbody>
</table>


### Exploring and changing files

These commands are the commands I feel improves my workflow the most and overall productivity when working on a project. Easy to remember and definitely a good place to start for beginners

<table>
  <thead>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ls</td>
      <td>List the files/folders in a directory</td>
    </tr>
    <tr>
      <td>ls -la</td>
      <td>List all the files/folders in a directory (including hidden files) and displays additional information about them</td>
    </tr>

    <tr>
      <td>cd pathname/directory/subdirectory</td>
      <td>To change directory</td>
    </tr>

    <tr>
      <td>cd ../</td>
      <td>To go up a level of a directory</td>
    </tr>
    <tr>
      <td>cd ../../themes/images</td>
      <td>Or you can chain these commands together to navigate across directories</td>
    </tr>

    <tr>
      <td>cp filename-to-copy.txt new-file-name.txt</td>
      <td>To copy a file with the same directory simply type</td>
    </tr>
    <tr>
      <td>cp filename.txt ../../new-directory/filename.txt</td>
      <td>To copy between directories:</td>
    </tr>
    <tr>
      <td>cp images/* ../skin/</td>
      <td>To copy all files from one directory to another, use the * character, which unofficially means all</td>
    </tr>

    <tr>
      <td>mv current-directory/file.txt ../new-directory/file</td>
      <td>Move a file</td>
    </tr>

    <tr>
      <td>mv oldfilename.txt newfilename.txt</td>
      <td>To rename a file, use the ‘mv’ but change the name of the file when stating the directory receiving the file.</td>
    </tr>
    <tr>
      <td>rm filename.txt</td>
      <td>To delete a file type</td>
    </tr>
    <tr>
      <td>rm -r folder</td>
      <td>Alternatively if you wish to delete a directory, and all directories and files within that recursively, type</td>
    </tr>
  </tbody>
</table>
