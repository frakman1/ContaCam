<p align="center"> 
<img alt="demo" width=100 src="https://github.com/frakman1/ContaCam/assets/5826484/9ccb434f-f5f0-4dd5-aa28-5601ecb8de6b"> 
</p>


---


- 🎥 This space is dedicated to fans of the [ContaCam](https://www.contaware.com/contacam.html) app and meant to be a landing page for anyone wishing to discuss ideas, raise issues or share use-cases and configurations with the ContaCam user community.

- 🐞 The ContaCam developer is right now on a tight schedule, for that reason, the app is temporarily in maintenance mode. It is unlikely that any new features will be added soon, but there may be patch releases to address minor bugs in the future. With that in mind, feel free to open issues in the [Issues](https://github.com/frakman1/ContaCam/issues) tab but don't expect much activity or resolution.

- ❓ For everything else that is not an actual bug, feel free to use the [Discussions](https://github.com/frakman1/ContaCam/discussions) tab as a forum for asking questions and having conversations around various ContaCam related topics.

- 🙋 Before raising issues or asking questions however, please consult the excellent ℹ️ [FAQ](https://www.contaware.com/manual-faqs.html) which address most concerns.
  

---

<p> 
<h1 align="center">Tips and Tricks</h1>
</p>

Here are a few tweaks that I make to the app to make it more functional. 
If you have any tips you'd like to share, feel free to add them in the [Discussions](https://github.com/frakman1/ContaCam/discussions) page and I will add it to this list.
<p>&nbsp;</p>

--- 
To increase the Web UI session timeout and avoid logging in all the time, change a couple of PHP parameters as described [here](https://www.contaware.com/manual-faqs/21-05-contacam-networking/119-increase-web-interface-session-timeout.html)

---

<p>&nbsp;</p>

---

 To get a direct, no-login URL to your Web UI, use a URL in this form (remember to [URL-encode](https://www.urlencoder.org/) any special characters in your password):

```bash
http://CONTACAM-PC1:PORT/?username=xxx&password=xxx
```

Similarly for an individual camera's feed: 

```bash
http://CONTACAM-PC1:PORT/CAMERA_NAME/push.php?username=xxx&password=xxx
```
---

<p>&nbsp;</p>

---

  To troubleshoot any issues, look at the ContaCam log file (found under Settings -> View Log File)
```bash
C:\Users\USERNAME\AppData\Roaming\Contaware\ContaCam\log.txt
```
 
Also check the micro apache (`mapache.exe`) web server's log files for issues with starting the webserver. Those are stored in the same folder:
```bash
C:\Users\USERNAME\AppData\Roaming\Contaware\ContaCam\httpd_log.txt
```
---

<p>&nbsp;</p>

---

To get bigger live snapshot thumbnails in the Web UI, you can change the size in the Camera Advanced Settings page:

![image](https://github.com/frakman1/ContaCam/assets/5826484/e9383693-51b2-4960-a1e7-29b1b6488295)

![image](https://github.com/frakman1/ContaCam/assets/5826484/1d246045-a2a6-4b7a-8aa8-196f163e65f6)

---

<p>&nbsp;</p>

---

To get more animated gifs in the recorded history page of a Camera, you can change the grid size by editing the `summarysnapshot.php` file in `C:\Program Files (x86)\ContaCam\microapache\htdocs`

Around line 60: (change to 42 instead of the default 12)
```php
// Max files per page, pages count and page offset
$max_per_page = 42
```
Around line 451: (change to 6 instead of the default 4)
```php
$max_container_width = 6 * $min_grid_width; // 12 responsive thumbs: 4 x 3, 3 x 4, 2 x 6 and 1 x 12
```

![image](https://github.com/frakman1/ContaCam/assets/5826484/d4dc156e-4823-4b54-96b1-c91b2fbe2da0)

---

<p>&nbsp;</p>

---

In ContaCam's FAQ, there is a [page](https://www.contaware.com/manual-faqs/20-06-contacam-advanced-tasks/98-externally-control.html) that describes turning on/off multiple cameras via the command line using each camera's `.bat` file located in its corresponding folder. This is useful if you want to stop excessive network traffic or CPU usage temporarily.

For example you'd make a new `.bat` file that calls all those individual cameras `.bat` files like this:

```batch
@echo off
call "C:\ContaCam\My Camera 1\CAMERA.bat" off
call "C:\ContaCam\My Camera 2\CAMERA.bat" off
call "C:\ContaCam\My Camera 3\CAMERA.bat" off
```
However, each camera has a built in delay of about 3 or 4 seconds that can get annoying to wait or have to press the keyboard to bypass.
Instead, you can make a `.bat` file (for example `turn_all_cameras_off.bat`) that calls each camera's corresponding `.bat` file in a new window (in parallel) so it keeps going without any delay like this:

```batch
start cmd.exe /c "C:\ContaCam\My Camera 1\CAMERA.bat" off
start cmd.exe /c "C:\ContaCam\My Camera 2\CAMERA.bat" off
start cmd.exe /c "C:\ContaCam\My Camera 3\CAMERA.bat" off
```

