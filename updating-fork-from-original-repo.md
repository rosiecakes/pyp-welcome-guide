# How to update your fork from the original repo

Suppose we make a change in the original repo of a group project. How do you get your own fork updated with those changes? This guide will help you with that. To do so, I'm going to use these repos as example:
* My fork: [https://github.com/santiagobasulto/pyp-w1-gw-language-detector](https://github.com/santiagobasulto/pyp-w1-gw-language-detector) (note my username in the URL)
* The original repo that I forked: [https://github.com/rmotr-group-projects/pyp-w1-gw-language-detector](https://github.com/rmotr-group-projects/pyp-w1-gw-language-detector)


# Step 1: Get the original's repo Clone URL

Go to the original repo (the one in `rmotr-group-project`'s organization) and get the clone URL:

![image](https://cloud.githubusercontent.com/assets/872296/15449558/5cddad8c-1f57-11e6-8fbb-51f7926baf18.png)

**Important:** Be consistent with the type of URLs you're using. The clone URL can be either SSH or HTTPS. In this example I'm using the HTTPS URL, but I can also choose to use the SSH URL. If you chose HTTPS to clone the repo in Cloud9, also choose the HTTPS version of the URL for this guide.

![image](https://cloud.githubusercontent.com/assets/872296/15449565/948078c8-1f57-11e6-89ee-479c540d49de.png)

# Step 2: Check your remotes

Git has the concept of different "remotes". Your fork is your main (and only) remote. You can see that by executing the following command:

```
git remote -v
```
![image](https://cloud.githubusercontent.com/assets/872296/15449580/faac64d6-1f57-11e6-9ed5-fcd539c5d9df.png)

# Step 3: Add the original repo as a remote

Use the following command to add the new remote:

```
git remote add [NAME-OF-REMOTE] [CLONE URL FROM STEP 1]
```

I'll use the name `upstream` to refere to the original repo, so, in my example this becomes:

```
git remote add upstream git@github.com:rmotr-group-projects/pyp-w1-gw-language-detector.git
```
![image](https://cloud.githubusercontent.com/assets/872296/15449589/3b53c90c-1f58-11e6-9e25-bec5733a2cf1.png)

# Step 4: Pull changes

That's it! Now you can pull changes from the original repo:

```
git pull upstream master
```

![image](https://cloud.githubusercontent.com/assets/872296/15449601/9aae7db6-1f58-11e6-860f-0b416b425168.png)
