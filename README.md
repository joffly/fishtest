Setup:
1. It's recommended to create a new user for running fishtest
  a. sudo useradd fishtest
  b. sudo passwd fishtest
2. su fishtest; cd ~
3. Clone fishtest
  a. git clone https://github.com/glinscott/fishtest.git
  b. Install latest version of celery
      i. git clone https://github.com/celery/celery.git
     ii. cd celery
    iii. python setup.py build
     iv. sudo python setup.py install
4. Install mongoClient
  a. sudo pip install pymongo
5. Set up testing directory
  a. mkdir testing
  b. Set environment variable FISHTEST_DIR to testing directory
    i. export FISHTEST_DIR=~/testing
    ii. Also, add to ~/.bash_profile
  c. cp ~/fishtest/scripts/timed.sh ~/testing
    i. Make sure to edit timed.sh to appropriate concurrency!  If you have a 4 core system, it should be -concurrency 3 for example.
  d. Get opening book and cutechess-cli
    i. TODO

6. Connect to the server, and forward ports locally (5555 for Celery Flower,
   27017 for MongoDB and 5672 for RabbitMQ):
ssh -v -f username@remote_host -L 5555:localhost:5555 -L 27017:localhost:27017 -L 5672:localhost:5672 -N

Launching the worker:
cd ~/fishtest
./start_worker.sh