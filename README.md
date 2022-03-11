# Video-Chatting-Website

Project idea – Create a simple chat app where you can create chat rooms and users will chat in real-time. You don’t need to store all the previous chat records as you can display only a few recent chats and older chats will be deleted.

# Architecture

When a user logs in, the frontend downloads the user list and opens a Websocket connection to the server (notifications channel).
When a user selects another user to chat, the frontend downloads the latest 15 messages (see settings) they've exchanged.
When a user sends a message, the frontend sends a POST to the REST API, then Django saves the message and notifies the users involved using the Websocket connection (sends the new message ID).
When the frontend receives a new message notification (with the message ID), it performs a GET query to the API to download the received message.

# Database
For this demo, I'm using a simple MySQL setup. If more performance is required, a MySQL cluster / shard could be deployed.

PD: I'm using indexes to improve performance.

# Assumptions
Because of time constraints this project lacks of:

User Sign-In / Forgot Password
User Selector Pagination
Good Test Coverage
Better Comments / Documentation Strings
Frontend Tests
Modern Frontend Framework (like React)
Frontend Package (automatic lintin, building and minification)
Proper UX / UI design (looks plain bootstrap)

# Run
move to project root folder

Create and activate a virtualenv (Python 3)

pipenv --python 3 shell
Install requirements
pipenv install
Create a MySQL database
CREATE DATABASE chat CHARACTER SET utf8;
Start Redis Server
redis-server
Init database
./manage.py migrate
Run tests
./manage.py test
Create admin user
./manage.py createsuperuser
Run development server
./manage.py runserver
To override default settings, create a local_settings.py file in the chat folder.

Message prefetch config (load last n messages):

MESSAGES_TO_LOAD = 15
