---
title: "Unleashing the Power of ChatGPT in Linux CLI: A Game-Changing Experience! 🤯👩🏻‍💻"
datePublished: Sat Apr 22 2023 13:04:36 GMT+0000 (Coordinated Universal Time)
cuid: clgs08azr00iu4ynvhcnk9wgi
slug: unleashing-the-power-of-chatgpt-in-linux-cli-a-game-changing-experience-b146637d7e7f
canonical: https://devangtomar.medium.com/unleashing-the-power-of-chatgpt-in-linux-cli-a-game-changing-experience-b146637d7e7f
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682169400766/a9c41f7f-31cf-4ed4-ad0d-776d093d291b.jpeg
tags: chat, chatgpt, chat-gpt, chatgptguide, chatgptplus

---

ChatGPT has transformed how individuals engage with technology. It has ushered in a new era of personalized and natural language communication, making it simpler for people to get things done, obtain information, and interact with others. ChatGPT has enabled more smooth and effective communication, resulting in a more comfortable and connected environment for individuals all over the world, from customer care chatbots to language learning apps.

Although ChatGPT has a fantastic user interface, there are some quick and easy ways to get this going for techies who prefer CLI to the GUI. Yes, you’re correct. Developers and the local community have created several packages and other materials that allow us to quickly load the CLI.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169386162/5216e710-a2f7-4552-b669-d8c10f4af3c7.jpeg align="center")

So let’s get going.

#### Pre-requisites 🐣

* A Linux machine or a virtual instance: You can obtain a Linux machine or a virtual instance from cloud providers like AWS, GCP, or any other provider of your choice.
    
* Python and PIP package manager: Python is an essential tool for running ChatGPT, as it is built on Python, and many other Linux tools and libraries are also built on Python. Python is usually preinstalled on most recent Linux distributions.
    

To check the Python version, use the command

```python
python3 --version
```

If Python3 is not installed, use the command (considering you are on Ubuntu)

```python
sudo apt install python3 -y
```

PIP is a package manager that works across platforms, which is used to install, upgrade, and uninstall the required packages. PIP is generally preinstalled with Python in most Linux distributions. To install PIP, use the command :

```python
sudo apt install python3-pip -y
```

And to check the PIP version, use the command

```python
pip3 --version
```

* Venv module (optional but recommended): The venv module is not required for ChatGPT, but it is recommended to create an isolated virtual environment in Linux and avoid conflicts with other libraries. To install the venv module, use the command
    

```python
sudo apt install python3-venv
```

And to create a virtual environment with venv, use the command

```python
python3 -m venv <virtual_environment_name>
```

For example :

```python
python3 -m venv chatgpt_linux_cli
```

* Virtual Environment Activation: Once you have created a virtual environment with venv, it will be deactivated by default. To activate the virtual environment, use the command
    

```python
source <virtual_environment_name>/bin/activate
```

Once you execute the above command, the shell prompt will now display the name of the virtual environment in brackets, like this:

```python
(<virtual_environment_name>)<username>@<system_name>
```

For example, the default Linux shell prompt will change to (`chatgpt_linux_cli`) upon running the commands above.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169387756/88ccfb5b-40fe-410b-9a70-68160d8e3dcc.png align="center")

#### Get Your OpenAI API Key 🔑

To utilize ChatGPT’s offerings in Linux, you will require an OpenAI API key. Presently, OpenAI is giving out $5 credits for testing purposes. Once the credits are utilized, payment must be made for API access. However, the following are the steps to acquire an OpenAI API key for this ChatGPT command line chatbot:

* Visit the [**OpenAI website**](https://platform.openai.com/signup) and register for an OpenAI account. Simply log in if you already have an account to go to the next stage.
    
* Next, select “**View API keys**” from the drop-down menu by clicking on your profile image in the top right corner of the screen.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169389212/16f35f7e-1cd4-4cda-937d-762c04e30754.png align="center")

* You can view all previously generated API Keys here, if any. Click the “**Create new secret key**” button to generate a fresh API key.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169391357/a5da7bf8-ba2e-4726-85ac-067b3a5388c5.png align="center")

* Your API key will appear in a fresh pop-up window. This API key should not be disclosed to the public or shared with anybody. You can only view your API key once, so be sure to copy it somewhere safe. If you click “OK” at this point, you won’t be able to copy the API key.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169392680/a7dc2cb6-fab6-4d9b-970c-d6ac9b4f724f.png align="center")

* Now, create an environment variable for this API key with the command below. In Linux, you can create an environment variable using the “`export`” command. Replace `<your_OpenAI_API_key_here>` placeholder with the actual API key you generated to use ChatGPT in the Linux terminal.
    

`export OPENAI_API_KEY=<your_OpenAI_API_key_here>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169394170/c7d1dc82-6459-43ab-89c6-f93a3d312bfd.png align="left")

> **Note** : You can verify the environment variable by listing it with the `env` command

* This variable is only temporarily stored for the current session. To store the API key permanently, open the `.bashrc` file in the text editor of your choice and add the variable at the end of the file.
    

```python
export OPENAI_API_KEY=<your_OpenAI_API_key_here>
```

* After adding the OpenAI API key, save the document and close the text editor. Run this command to make the changes effective right away:
    

```python
source .bashrc
```

> **Note** : Finally, verify the changes with the env command `env`

#### Install ShellGPT to Use ChatGPT ⚙️

After completing the environment setup, you can now install ChatGPT for Linux using the command line. If you’re setting up the installation in a virtual environment, you must remove the `--user` flag. Use the following command to now install ShellGPT on your computer:

```python
pip3 install shell-gpt --user
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169396360/fe8293cb-2461-41b4-8f24-92efb460255b.png align="left")

#### ShellGPT: Syntax & Options ⭕

You must be anxious to utilise ShellGPT for a variety of tasks now that you have installed it. But first, let’s look at the syntax and a few options we have to employ to spice up our outputs. ShellGPT’s simple syntax makes it simple to use for numerous tasks:

```python
sgpt <options> <input_query>
```

You can use the ShellGPT (`sgpt`) chatbot to, among other things:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169397800/4e783c8b-6fc4-40d0-848a-748bbb87d570.png align="left")

### How to Use ChatGPT in Linux Terminal (Examples) 👩🏻‍💻

#### 1\. Use ShellGPT for Queries ⁉️

For any kind of search, you can utilise ShellGPT as the search engine. Since it is an AI chatbot, the results are more human-like rather than a list of ranked web pages like you would typically get from a search engine. To utilise ShellGPT to retrieve answers to your queries, use the following syntax:

```python
sgpt “<your_query>”
```

Use this command, for instance, to determine the mass of the sun:

```scss
sgpt "mass of sun"
# -> = 1.99 × 10^30 kg
```

#### 2\. ChatGPT Chatbot Mode 📳

If you’ve ever utilised ChatGPT for chat, you must have thought that the responses were on par with those of a real person. You may now utilise ChatGPT directly from your Linux terminal thanks to ShellGPT. Use just the `— chat` option, a special session name, and a prompt.

```scss
sgpt --chat number "please remember my favorite number: 4"
# -> I will remember that your favorite number is 4.

sgpt --chat number "what would be my favorite number + 4?"
# -> Your favorite number is 4, so if we add 4 to it, the result would be 8.
```

#### 3\. Generate Code 🧑🏻‍💻

You can also use chat sessions to iteratively improve GPT suggestions by providing additional clues.

```python
sgpt --chat python_requst --code "make an example request to localhost using Python"
```

```python
import requests
response = requests.get('http://localhost')
print(response.text)
```

Asking AI to add a cache to our request.

`sgpt --chat python_request --code "add caching"`

```python
import requestsfrom cachecontrol import CacheControl
sess = requests.session()cached_sess = CacheControl(sess)
response = cached_sess.get('http://localhost')
print(response.text)
```

#### 4\. Generate Shell Commands 💻

While the Terminal can be a powerful tool for automating operations and running complex commands, it can occasionally be challenging for new users to recall the syntax and options of different [Linux commands](https://www.javatpoint.com/linux-commands). You can use ChatGPT on your command line to obtain not just the syntax of a Linux command but also the precise command along with any necessary parameters and options. Use the`--shell`flag as follows:

```python
sgpt --chat sh --shell "What are the files in this directory?"
# -> ls
sgpt --chat sh "Sort them by name"
# -> ls | sort
sgpt --chat sh "Concatenate them using FFMPEG"
# -> ffmpeg -i "concat:$(ls | sort | tr '\n' '|')" -codec copy output.mp4
sgpt --chat sh "Convert the resulting file into an MP3"
# -> ffmpeg -i output.mp4 -vn -acodec libmp3lame -ac 2 -ab 160k -ar 48000 final_output.mp3
```

> More here : [GitHub — TheR1D/shell\_gpt: A command-line productivity tool powered by ChatGPT, will help you accomplish your tasks faster and more efficiently.](https://github.com/TheR1D/shell_gpt)

#### Conclusion 💭

Therefore, ShellGPT incorporates ChatGPT’s power into your Linux terminal.For both inexperienced and seasoned users, it not only makes command-line work simpler but also introduces new functionality.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682169399111/227f1e82-c523-4d4d-adaf-db93b575e047.jpeg align="left")

Additionally, as was already mentioned, it gains in usefulness over time because it is built to learn from users.

Remember, though, to never give any AI model your company’s confidential code or any other sensitive data. Having said that, please share your thoughts on this command-line AI tool in the comments section below.

#### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)