---
layout: post
category : blog
title :  Flask  project EMU
tags : [ Flask , Python ]
---

###project EMU is for train ticket_booking , I have done this project with java before, now I change it to python with Flask 

###Part One : database tables

##### their are five tables , `Admin` is for admin to manage the system; `user` is for user to sign in  and register his accounts; `Train` is for train information, such as `train ID`, `volume`,`train type`,`train number`; table `Ticket` is for  info of tickets ,such as `ticket ID`, `start Date` , `end Date`, `start place` , `end Place` ,`price`, `seat number`,`train ID`; `User_booked_ticket` is for making user's booking tickets, such as `train ID` and `ticket ID`

###part Two : create a project 

to install flask if we don't have. 

` sudo easy_install virtualenv`

#####cerate and active its environment：

`mkdir emu`,`cd emu`,`virtualenv env` , the use ` . env/bin/activate` to active. and finally , use `easy_install Flask` to install flask in this ENV.


----------------------------------------------


###Part Three : add code.

#####create  file named "emu.py",

we need these Plug-in: 

`flask_mail` for sending emails;

`flask_principal` for managing permissions;

`flask_uploads` for uploading file;

`flask_wtf` for preventing duplicate submissions of the form(named "CSRF"?) and recaptcha.


#####`@app.route('/')`

`def index():`

`    return render_template('index.html')`

this page for index view, and if user login in , he can get this page.

#####`@app.route('/user/sign_up',methods=['GET', 'POST'])`

for user to sign up.


#####`@app.route('/user/<ticket_number>',methods = ['GET',"POST"])`

`def book_ticket(ticket_number):`

for user to book a ticket.

#####`@app.route('/user/logout')`

`def logout():`

for user to logout

#####`@app.route('/user/ticket_list',method ='GET')`

`def show_user_ticket():`

for listing user booked tickets

`def delete_user_ticket(): `

if user has a ticket whick he doesn't want, he can delete it .


#####`@app.route(/user/register,method = "POST")`

`def user_register():`

for user to register his account

#####`@app.route(/admin/login,method = 'POST')`

`def admin_login():`

for admin to login.

#####`@app.route(/admin/logout)`

`def admin_logout():`

for admin to logout.

####`@app.route(/admin/index)`

`def admin_remove_user():`

for admin to remove user.

`def admin_add_user():`

for admin to add user accounts.


#####`@app.route('/user/upload', methods=['GET', 'POST'])`

`def user_upload_file():

` if request.method == 'POST':`

` f = request.files['the_file']`

`f.save('/var/www/uploads/' + secure_filename(f.filename))`
 
