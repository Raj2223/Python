# Python
Projects

Overview
Introduction
What is Whatsapp automation using python?
What are its features?
Let’s code!
Errors and exceptions
Handling error
Can we do it another way?
Conclusion
 Introduction
Imagine, you turned on your pc, a message “Good Morning!” is automatically sent to your WhatsApp contact without having done anything. And this is what we are going to create and with various other features.

What is Whatsapp Automation Using Python?
It is a utility and the best python software that will save your time and will make you a punctual person in other person’s views. It will basically automate WhatsApp web and send the message.

What are its Features?
So let’s understand it backwards, what are its features and how will it work.

You turned on your pc,

This program will run automatically
Wait for 2 minutes to not load to pc (as many programs run simultaneously when a pc starts like antivirus programs and many more which slows down the pc and this program will wait to not load the pc)
Check the file (database of the program)
If it does not exist,
it will create the file and will send the message and then update the file.
if it exists,
Then, will check if the last date (the database will have the dates of the message sent ) is of another year and if yes it will delete all the contents of the file (to free up the space taken by it) and will send the message and it will again update the current date to the file.
And if the last date’s year is the same as the current year, it will directly move forward.
If the last date in the file is not the current date, then it will send the message and update the database.
And if the last date in the file is the current date, then it will just check for the last year’s date and will close the program.
If there is a problem in sending the message, it will not update the database and will notify the user that there is a problem in sending the message.
whatsapp automation
Whatsapp logo

Loading Image
Build an AI model to Save Lives.
Win exciting prizes worth 2.5L+($3000+) 09-18th Dec 2022
Let’s code!
As we have known all the things that our program will do. So now we will start creating our program.

First of all, we will need to download the modules/libraries required to work with the program

And the modules are “time”, “datetime”, “selenium”, “os”, “plyer”

Out of all these modules, only Selenium (here its version: 3.141.0) and plyer (here its version: 2.0.0) module needs to be downloaded and other remaining comes preinstalled with python 3.

So using this command in this terminal, you can download and install all these modules.

pip install selenium plyer
Now we have installed the modules and now we can import them into our program and use it. And below we will start our coding.

import time
time.sleep(120)
import datetime 
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
import os
from plyer import notification
As we will make our program automatically started at the start of the pc, we will make our program sleep for 2 minutes to not load on our pc (As explained in the what are its features section ).  On the first line of our program, we have imported the time module then in the second line, we made our program sleep. And line after line we will import all the modules like in third line, datetime module, fourth line webdriver class from selenium and in next line options from selenium and again in next line Keys from selenium and after that, we have imported os module and at last, we have imported notification from plyer (Same as our infinite timer using python program ).

Below is why we are importing all these modules

time – mainly for making our program sleep
datetime – To work with dates and years (To update the database)
webdriver – It is used to work with the browser and the website
Options – It is used to add arguments to the browser like which extensions to use and which user account to use and maximize the window and much more.
Keys – It is used to work with the keys of the keyboard or hotkeys like Ctrl+A and Ctrl+C or Enter.
os – Exiting the program
notification – For notification (If an error occurs while sending the message, as explained in what are its features section )
Note: YOU CAN ADJUST THE SLEEP TIME ACCORDING TO YOUR CONVENIENCE. IF YOUR PC IS ALWAYS CONNECTED TO A WIFI OR ETHERNET, THEN YOU CAN DECREASE THE SLEEP TIME OR IF YOUR PC IS FAST ENOUGH, THEN ALSO YOU CAN DECREASE THE SLEEPING TIME AS IT IS DEPENDENT ON PC TO PC.

Now the main messenger() function starts here

def messenger():
    try:
        url ="https://web.whatsapp.com/send?phone=+91xxxxxxxxxx"
        message_content = "Good morning!"
        path = r"<your chrome driver path>"
        options = webdriver.ChromeOptions()
        options.add_argument("user-data-dir=<Your_browser_user_profile>")
        driver = webdriver.Chrome(executable_path=path, options=options)
        driver.minimize_window()
        driver.get(url)
        time.sleep(20)
        type_it = driver.find_elements_by_class_name('_13NKt')
        time.sleep(20)
        try:
            type_it[1].send_keys(message_content + Keys.ENTER)
        except IndexError as e:
            time.sleep(20) 
            type_it = driver.find_element_by_xpath('/html/body/div[1]/div[1]/div[1]/div[4]/div[1]/footer/div[1]/div/span[2]/div/div[2]/div[1]/div/div[2]')
            type_it.send_keys(message_content+ Keys.ENTER)

           
            print(e)
         time.sleep(10)
        driver.quit()
    except Exception as e:
        notification.notify(
            title = "Whatsapp message not sent",
            message = "Error while sending!",
            app_icon = r"<Your icon file>",
            app_name = "Whatsapp Message error",
            toast = True,
              )
        print(e)
        os._exit(0)
In the first line of the above code, we have defined the messenger() function. Since in the automation process, there may be some errors ( like internet problems or any other issue ). So we will use try-except block to make our program error-free.

Therefore, we have to use the try method in the second line. In the next line, we have created the variable url which will contain the url of the Whatsapp web ( Url will contain the phone number of the person to whom you want to send the message ). And in the next line, we have the variable message_content ‘ (You can change it as you want) which will contain the message to be sent.

And in the next line, we have the variable message_content which will contain the message to be sent. The next line contains the path variable which will contain the path of the chrome driver (Note: The ‘r’ (r is used for raw string )behind string is used to not escape the escape characters, like ‘/n’ is used to get a new line and if you want to print it, then it will not get printed, just a new line will be printed. To print it, we can use either ‘//n’ or r’/n’, Both will print the characters ‘/n’. And in a path like ‘C:/users’, ‘/’ may raise any issue, so we are using it for raw string ). More about the path in the handling section. 

BONUS: You can’t use WhatsApp Web without scanning the QR code. You have to scan the QR minimum of 1 time and then if you checked the keep me signed in option, you can visit the site directly without scanning the QR again. And if you are using another profile of the browser which doesn’t have WhatsApp logged in, then you have to scan the QR again. But what you can do is just join the beta mode of WhatsApp, and you will have no issue sending the message. More on this in the handling error section.

In the next line, we have variable ‘options’ which will contain the ChromeOptions(). It is just used to work with the profiles, extensions, cookies or proxies, and stuffs like that on the browser. In the next line, we have added the argument which contains the profile in which WhatsApp is logged in. In the next line, the driver variable is used which initializes the Chrome with the chrome driver as specified above and the options for the profile as an argument.

In the next line, we have minimized the screen for just working in the background type. Next, we have a driver variable that will get the URL in the browser. Now we will make our program sleep for 20 seconds to not get any error in accessing the elements of the site (As the website may take time to load and elements of the site may not be loaded quickly). In the next line, we have variable type_it, which will contain the list of the elements of the given class name of the element. NOTE: THE CLASSES AND XPATH MAY HAVE CHANGED WHEN YOU ARE READING THIS, SO FIND YOUR CLASS NAME FOR THE TYPING BOX AND THEN USE IT. Again we will make the program sleep for 20 seconds. Then we will use the second element from the list for sending the message and will use keys. ENTER to send the message using Keys that we have imported earlier. We will use try and except because sometimes it is not able to access the element and will throw the Indexerror. And if it happens, we will try it again and then send it using its ‘Xpath’. After that, we will make our program sleep, as if it is sent from our program but due to instant use of quit method to quit the driver, it may not send it sometimes.

And if any error happens in sending, then it will simply send the user a notification. For that, we have to use notify function of the imported notification from the plyer module. As we have done in infinite timer using python, we will send the desktop notification to the user. To know more about what is done here, just refer to another article which is infinite timer using python. At the last of the error happened, we will just quit the program as we don’t need to do any work now. So we will use the _exit(0) function of the os module with ‘0’ to say everything is fine in the program to the system.

Now we have to work only on the database section.

today = str(datetime.date.today())
today_2 = f"{today} "
content = bytes(today_2,'utf-8')
year_str = str(datetime.datetime.now().year)
year_edit = bytes(year_str,'utf-8').decode('utf-8')
date_str = str(datetime.datetime.now().day)
date_edit = bytes(date_str,'utf-8').decode('utf-8')
edit = {"1":"01",
        "2":"02",
        "2":"03",
        "4":"04",
        "5":"05",
        "6":"06",
        "7":"07",
        "8":"08",
        "9":"09",}
print(date_edit)
try:
    file = open("database.txt", "x")
    messenger()
    file.write(today_2)
    file.close()
except Exception as e:
    file = open("database.txt", "a+b")
    try:
        try:
            file.seek(-11,2) # seek will not work in negative in text mode, only in byte mode
        except OSError as e:
            print(e)
            messenger()
            file.write(content)
            file.close()
            os._exit(0)
        year = file.read(10).decode('utf-8')
        file.seek(-11,2)
        date = file.read(10).decode('utf-8')
        if year_edit != year[:4]:
            file.close()
            file = open("database.txt", "wb")
            file.close()
            file = open("database.txt", "a+b")
            messenger()
            file.write(content)
            file.close()
        for x in edit.keys():
            if x == date_edit:
                date_edit = edit.get(x)
                break
        if date_edit != date[8:14]:
            messenger()
            file.write(content)
            file.close()
            os._exit(0)
    except Exception as e:
        print(e)
Now the main thing is we will use datetime module to get the date, year, and all. Since datetime object is of type ‘datetime’ not ‘str’ (string in python ), there will an error in writing this to the file. So we have to convert it to ‘str’ and also we have to convert all these to bytes to read and write in the file in bytes mode. But one of the bugs of the datetime module in our program can be the dates, like the date, 2022-01-01 will be 2022-1-1 as per datetime module. Now if we check the last date in our database to check if the message was sent on that date or not, we will get a wrong answer as both are different. So we will fix this bug by making a dictionary of the digits (technically string) to that of the required digit (Again string).

As said in What are its features section?
If there is no database file in that directory, it will directly create the file and will call the messenger() function and will send the message and then update the current date to the database. And then close the file and the program will end.
NOTE: YOU MUST CLOSE THE FILE AFTER OPENING IT BECAUSE SOMETIMES IT DOESN’T SAVE THE FILE AND YOUR WORK WILL NOT BE DONE.

And if there is an error like there is the database already in the directory, then it will directly enter into except block and will open the file in read + write mode in bytes like “a+b”.

Now if the file is empty, then seeking the file pointer anywhere will throw OSError, and messenger() function will be called and it will update the database with content in bytes as we have opened it as ‘b’ or bytes. And then the file will be closed and the program will be exited.
And if the file has contents, then it will read the year and decode it to normal encodings which is ‘utf-8’ and then we will seek the file pointer to a position from where it can read the specific date in the file and again decode it.

First, it will check if the year in the file is not the current year, then it will close the file opened in ‘appending and reading in bytes mode’ and then open it in writing and bytes mode (it will clear all the contents of the file ). Then it will simply close the file as all contents are deleted from the file and then we will again open the file in ‘a+b’ mode and call the messenger() function and then update the file with the current date and then close it. And the program is closed now.

The bug we have solved above will be used, using for loop it will change the contents of the date_edit variable using the dictionary keys.

At last, it will check if the date on the file is not the same as the current date, it will simply call the messenger() function and update the file, and will close it.
And if there is an error while the running of the program, it will simply handle it and will print the problem.

Now some of you may want to send messages to any groups or other contacts. To do this, you can search the contact in the type_it[0] and then click the result and again do the same to send the message as we have done in our program.

Errors and Exceptions
You will have an error when WhatsApp will not load or will ask for QR. Or your chromedriver is of another version as of your chrome version.

This program may not send messages every time.

Reasons

Due to improper internet connection
Due to not working of webdriver
Due to high usage of ram in the background
And these may not notify you about the message not be being sent because according to our program all these will be handled by our webdriver and it will not get into exception handling. But every time you start your pc, it will try to message if it is not sent.

 

Exception Handling
You can join Whatsapp beta to manage the QR error. To join beta mode on WhatsApp, you can read this article

Chromedriver

It is only used for handling and testing chrome for developers.
First of all, you have to check for the version of your chrome and then just google for the chromedriver of that version and then download it and you are all done.

Tip: YOU CAN’T USE YOUR WHATSAPP WEB PROFILE  WHEN THIS PROGRAM IS RUNNING OR THE PROGRAM WILL CRASH. SO YOU CAN CHANGE THE SLEEP TIME OF THE PROGRAM ACCORDINGLY.

So in case you want to use the browser, you have to use another browser, not the browser that our program will use.

And yes, you can regulate the sleep time of your program according to your pc, ram, internet connection.

 

Can we do it another way?
Yes, but no! This software which is made manually can be replaced by various modules. But all those modules will have the same kind of code or maybe different from ours but we can use it. It is like we bought noodles and cooked them or we can just make raw noodles ourselves and then cook them. In both cases, we have cooked noodles, but by buying and cooking, it becomes hassle-free but you can’t add flavor to that raw noodle, on the other hand making noodles on our own takes time and sometimes hassles, but it is worth doing as you can do what you want with your raw noodles. So there are many alternatives to this and one of which is pywhatkit. It is also a very lightweight, easy to use, and fantastic module that is also worth practicing. I will definitely try to make an article on this in the future.

Conclusion
Woohoo! you made your own beast WhatsApp automating software with its own database.

Now you must try it yourself to fully enjoy the simplicity of python.

There is no specific output of this program but this is the image of the message sent.


snapshot of the sent message

 

Now we will make our program run automatically at startup.
To do this in windows, the steps are following.

Create a shortcut of your program (python file) > copy the shortcut file > press window-key+r > type shell:startup > press enter > Paste the shortcut file.

Now your program will run automatically at the startup of your computer
