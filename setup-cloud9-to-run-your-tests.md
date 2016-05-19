# Run your tests in Cloud9

## Step 0 - Install virtualenv

We'll be installing all our dependencies inside a virtualenv, to do so run the following command in C9's shell:

```
sudo pip install virtualenv
```

![image](https://cloud.githubusercontent.com/assets/872296/15372674/f2935ed6-1d17-11e6-8a14-2e6835ab7a73.png)

## Step 1 - Create a virtualenv

Choose a name and create your virtualenv. In this example, I've named my virtualenv `rmotr_group_project`. To create the virtualenv just use this command:

```
virtualenv rmotr_group_project # Replace with the name you want
```
![image](https://cloud.githubusercontent.com/assets/872296/15372762/622bb0ae-1d18-11e6-8499-c9124b25509a.png)

A virtualenv is just a directory with some special files inside. You can see how I have now a directory named `rmotr_group_project` and I can see it in the tree view:

![image](https://cloud.githubusercontent.com/assets/872296/15372842/ddd65358-1d18-11e6-91b4-ee086f99d719.png)

**Important:** Make sure you add the virtualenv name to the _.gitignore_ file, so you don't push it to Github. Virtualenvs are supposed to be local.

**Hint:** By default, the virtualenv is created with the default python interpreted. You can choose to create your virtualenv using a different Python interpreter with the `-p` option. For example, using python3:

```
virtualenv rmotr_group_project -p /usr/bin/python3
```
![image](https://cloud.githubusercontent.com/assets/872296/15400429/dead85d6-1dc1-11e6-9d71-818e937ba9ca.png)


## Step 3 - Activate your virtualenv

**IMPORTANT**. This step is key. A virtualenv should be "activated". When we "activate" a virtualenv, we're changing the way our Python modules will be loaded. That means that, if at any point you're having issues, you need to make sure you have your virtualenv actiated.
To activate a virtualenv we'll be using the `source` command, and passing it the location of the "activate" file inside our virtualenv. Supposing my virutalenv is named `rmotr_group_project`, the command would be:

```
source rmotr_group_project/bin/activate
```

The _activate_ script will always be located inside the `bin` folder.

**When your virtualenv is activated,** you'll see the name of it, surrounded by parenthesis in the shell prompt, as you can see in this example:

![image](https://cloud.githubusercontent.com/assets/872296/15372980/853ebbb2-1d19-11e6-83ab-17c8f5335d7c.png)

## Step 4 - Investigate your virtualenv

Being inside a virtualenv means that the Python executable is different from the regular one used by the computer. That will allow us to install our own libraries inside the virtualenv without having conflicts with other users. Run the following command to see where the Python interpreter is located:

```
which python
```

If you pay attention, you'll notice that `python` is now located inside the virtualenv directory. Please, also notice that the venv is still active. A virtualenv will remain active, unless you explicitly deactivate it with the `deactivate`command.

![image](https://cloud.githubusercontent.com/assets/872296/15373028/d8591338-1d19-11e6-8f3f-2f5b4251a6ab.png)

## Step 5 - Install the requirements

**Make sure your virtualenv is active** and run the following command:

```
pip install -r dev-requirements.txt
```

![image](https://cloud.githubusercontent.com/assets/872296/15373109/5bcee940-1d1a-11e6-8e7b-411a508e9457.png)

## Step 6: Run your tests

By default, the group projects will have a `Makefile` that can be used to run the project tests. Just use the command `make test` or `make test-cov` (if you want to include a coverage report). **Make sure your virtualenv is active**

![image](https://cloud.githubusercontent.com/assets/872296/15400703/d183973c-1dc2-11e6-8958-0c4c1213585f.png)

## Step 7: Run tests in multiple Python versions

Just invoke the `tox` command. As simple as that. Just type `tox` in your console (with the venv active):

![image](https://cloud.githubusercontent.com/assets/872296/15400751/04b94714-1dc3-11e6-8c91-0065f7b878c2.png)

## Extra: Configure your own Cloud9 Runner

We'll confgure our own code runner in C9, which will allow us to use the beloved "Run" green button at the top to run our tests. To do so go to the Menu and click on "Run > Run With > New Runner (at the bottom of the list)" as you can see in the following image:

![image](https://cloud.githubusercontent.com/assets/872296/15405589/e315c072-1dd8-11e6-9e17-03d0036f5966.png)

A new tab will be opened and it should look something like this: 

![image](https://cloud.githubusercontent.com/assets/872296/15405637/18d5ddbe-1dd9-11e6-9127-6b6403686957.png)

To create a Runner that will run all your tests, paste this content:

```json
{
    "cmd": [
        "bash",
        "--login",
        "-c",
        "source rmotr_group_project/bin/activate && make test"
    ],
    "info" : "Started $project_path$file_name",
    "env" : {},
    "working_dir": "$project_path",
    "selector" : "source.ext"
}
```
**Important:** Make sure you include the name of your virtualenv. I'm using `rmotr_group_project` in the previous code.

Save your runner, you'll be prompted with a save dialog, choose the name you want (I'm choosing Make Runner) and just click "Save":

![image](https://cloud.githubusercontent.com/assets/872296/15405728/79029150-1dd9-11e6-8379-f8db590f6f53.png)

That's it! The runner should work. To run your tests, go to the Menu: "Run > Run With" and select your runner from the list ("Make Runner" in my example):

![image](https://cloud.githubusercontent.com/assets/872296/15405769/b9228a6a-1dd9-11e6-8f1f-5bc108c813da.png)

You can create as many runners as you wish. For example, you could create a runner to use the Python version of your virtualenv instead of the one used by default.

(Extra docs on runners: [https://docs.c9.io/docs/custom-runners](https://docs.c9.io/docs/custom-runners)
