#Tripwire


- Install Tripwire
    - *sudo apt-get install tripwire*
- Answer yes to the questions
- Create site key and local key
- Create policy file
    - *sudo twadmin --create-polfile /etc/tripwire/twpol.txt*
- Initialize the database
    - *sudo tripwire --init*
- Display the results in a file
    - *sudo sh -c 'tripwire --check | grep Filename > test_results'*
- Comment out the entries in twpol.txt that are also in test_results
- Recreate the encrypted policy file
    - *sudo twadmin -m P /etc/tripwire/twpol.txt*
- Repeat these 2 steps if there are still problem when recreating the policy file
- Reinitialize the database
    - *sudo tripwire --init*
- Run a check
    - *sudo tripwire --check*
- Delete test_results and twpol.txt
    - To recreate twpol.txt: *sudo sh -c 'twadmin --print-polfile > /etc/tripwire/twpol.txt'*
- Review and "Okay" the changes made to the system
    - *sudo tripwire --check --interactive*  (delete the cross if not okay with the change)
 - Add a crontab
    - *sudo crontab -e*
    - * 30 3 * * * /usr/sbin/tripwire --check | mail -s "Tripwire report for `uname -n`" email@mydomain.com*

- Update Tripwire after software change
    - **sudo tripwire --check --interactive**
