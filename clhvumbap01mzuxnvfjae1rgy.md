---
title: "Transcribing YouTube Videos using OpenAI’s Whisper📽️🗣️"
datePublished: Fri May 19 2023 18:49:19 GMT+0000 (Coordinated Universal Time)
cuid: clhvumbap01mzuxnvfjae1rgy
slug: transcribing-youtube-videos-using-openais-whisper-efb88f-efb88f-a29d264d6fb1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684578623829/ca6b4d24-1dc0-461b-b948-d3c6699d02c0.jpeg
tags: youtube, ml, ai-tools, transcription, whisper

---

Although [YouTube](https://www.youtube.com/) has emerged as the standard for video sharing and information gathering, not everyone has the time or capacity to watch a video through to the end. A tool for transcribing these movies can be useful in these situations. Today, we’ll look at how to use AI to create your own YouTube transcriber.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684578617396/a0e56ed9-1615-43d0-975b-6cd0f741f551.jpeg align="center")

We’ll also look at how Replicate may be used to scale up and offload the transcription process, as well as how to use natural language processing to summarise the finished video transcription.

#### **What is OpenAI’s Whisper? 🗣️🤖**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684578618997/68229b44-c6a4-4dab-8675-bcb5cec11a99.png align="center")

[Whisper](https://openai.com/research/whisper) is “an automatic speech recognition system trained on multilingual and multitask supervised data” created by OpenAI. It transcribes audio and video footage with astounding accuracy using cutting-edge deep learning models, making it simple to glean insightful information from massive amounts of spoken data.

Whisper has a wide range of potential uses, but we’ll be using it especially to record audio from YouTube videos.

#### **Getting started 👶🏻**

For these examples, Python 3 will be used because Whisper is available in this dialect.

#### **Virtual Environment Setup 🏞️**

Generally speaking, it’s a good idea to separate your package installations when starting a new Python project. By building a virtual environment, we may do this.

```python
python3 -m venv venv
```

This will create your virtual environment in a folder called `venv`. From here, we can then activate it:

```python
. venv/bin/activate
```

#### **Installing Dependencies 📦**

We’ll use `pip` to install the packages needed:

```python
pip install openai-whisper openai yt-dlp
```

1. [openai-whisper](https://github.com/openai/whisper) — Whisper model and API
    
2. [openai](https://github.com/openai/openai-python) — GPT-3 interface for natural language processing
    
3. [yt-dlp](https://github.com/yt-dlp/yt-dlp) — library for extracting YouTube data
    

#### **Fetching the YouTube Audio Stream 📽️**

To give us something to work with, I’ve provided a short example video below of a TED-Ed video.

<iframe src="https://www.youtube.com/embed/bFIVYRfyb3E?feature=oembed" width="700" height="393"></iframe>

We can then extract the data streams and remove the audio from the video using the video ID:

```python
import yt_dlp

def download(video_id: str) -> str:
    video_url = f'https://www.youtube.com/watch?v={video_id}'
    ydl_opts = {
        'format': 'm4a/bestaudio/best',
        'paths': {'home': 'audio/'},
        'outtmpl': {'default': '%(id)s.%(ext)s'},
        'postprocessors': [{
            'key': 'FFmpegExtractAudio',
            'preferredcodec': 'm4a',
        }]
    }
    with yt_dlp.YoutubeDL(ydl_opts) as ydl:
        error_code = ydl.download([video_url])
        if error_code != 0:
            raise Exception('Failed to download video')

    return f'audio/{video_id}.m4a'

def main():
    # The video ID of the embedded video above. 
    file_path = download('bFIVYRfyb3E')
```

This will download the above video as `audio/bFIVYRfyb3E.m4a`

#### **Transcribing the Audio File 🤖**

Now that we have the audio file on hand, we can simply feed it into Whisper:

```python
import whisper
# You can adjust the model used here. Model choice is typically a tradeoff between accuracy and speed.
# All available models are located at https://github.com/openai/whisper/#available-models-and-languages.
whisper_model = whisper.load_model("base.en")

def transcribe(file_path: str) -> str:
    # `fp16` defaults to `True`, which tells the model to attempt to run on GPU.
    # For local demonstration purposes, we'll run this on the CPU by setting it to `False`.
    transcription = whisper_model.transcribe(file_path, fp16=False)
    return transcription['text']

def main():
    transcript = transcribe('audio/bFIVYRfyb3E.m4a')
    print(transcript)
```

This will generate the full transcript for the video:

<details data-node-type="hn-details-summary"><summary>Video to text</summary><div data-type="detailsContent">Imagine that your life began roughly 300,000 years ago as one of the planet’s first humans. At this time, you live in Africa near modern-day Morocco, and your life isn’t too different from that of your hominid parents. You make crude tools, hunt, and gather food and materials, until, eventually, you perish. But this is only the beginning.Because after dying, you travel back in time to be reincarnated as the second human ever to live. While you don't remember your former life, your previous actions affect you nonetheless. And after dying once more, you return as the third person, then the fourth, the fifth, and so on—living the lives of every single human that’s ever walked the Earth. Strung end to end, these lives last almost 4 trillion years. Since you only recall the life you’re currently living, your psyche doesn’t carry the entire weight of human history. However, each of your lifetimes still has a profound impact on your future selves.Sometimes your influence on the world is obvious, but these major historical figures only account for a tiny fraction of your experience. Instead, your existence consists mostly of ordinary lives, filled with everyday tasks like eating, laughing, working, and worrying. For approximately one tenth of your 4 trillion years, you’re a hunter-gatherer. For 60%, you’re an agriculturalist, developing tools and techniques which you employ over roughly 800 billion years of working on farms. Across your lifetimes, you spend 1.5 billion years having sex and another 250 million years giving <a target="_blank" rel="noopener noreferrer nofollow" href="http://birth.In" style="pointer-events: none">birth.In</a> total, 20% of your existence is spent raising children, to whom you impart a variety of cultural values that influence the trajectory of generations. In some lives, you shatter those cultures through invasion and imperialism. In others, you suffer as your lands and loved ones are taken away. In over 1% of lives, you’re afflicted with malaria or smallpox, while, in others, you treat these conditions—saving countless versions of <a target="_blank" rel="noopener noreferrer nofollow" href="http://yourself.In" style="pointer-events: none">yourself.In</a> humanity’s early days, the average lifespan is fairly short. There are fewer lives to live, and your influence is usually limited to people physically near you. But as humans survive longer on average and Earth's population grows, you start to spend more time reliving the same action-packed years. A full third of your existence comes after 1200 CE, and a quarter of it takes place after 1750. At this point, technology and society start changing faster than <a target="_blank" rel="noopener noreferrer nofollow" href="http://ever.You" style="pointer-events: none">ever.You</a> invent steam engines, configure factories, and generate electricity, which power the daily machinery of all of your later lives. You live through revolutions in science, the deadliest wars in history, and dramatic environmental destruction. On average, each new life lasts longer, but the pace of your existence keeps accelerating. Conversations that previously took months to unfold now happen in minutes. Business ventures that you built over generations transform overnight. You enjoy luxuries you never could have sampled before, even in your past lives as kings and queens.After living over 100 billion lives, you're finally reborn as the youngest person alive today. But despite living through 300,000 years of human history, your actions have more impact today than 99% of your past lives. High-speed air travel allows you to carry contagions and cures across an ocean in hours. And the internet makes your personal sphere of influence global, allowing you to collaborate with anyone, anywhere, without even leaving your <a target="_blank" rel="noopener noreferrer nofollow" href="http://home.In" style="pointer-events: none">home.In</a> recent lives, you’ve invented tools to rewrite the genes of living organisms, permanently altering their future generations. And in this life, you might create even more technologies that make the world safer, kinder, and more equitable for for countless future lives.However, one careless invention could just as easily be catastrophic.Between nuclear weapons, lab leaks, climate change, and other existential threats,humanity's risk of inducing our own extinction has never been <a target="_blank" rel="noopener noreferrer nofollow" href="http://higher.In" style="pointer-events: none">higher.In</a> this fast-paced, interconnected world,it’s frighteningly easy to undo all of humanity’s progress,or potentially, cut short all your possible futures.There's no way to know what will happen next.But what’s clear is that your potential is <a target="_blank" rel="noopener noreferrer nofollow" href="http://limitless.So" style="pointer-events: none">limitless.So</a>, how will you spend this life? And what can you do to work towards a better future for all your lives to come?</div></details>

#### **Generating a Transcript Summary 📃**

In their videos, many YouTube creators incorporate sponsorships, adverts, and filler content. With the aid of natural language processing, we can create a transcript summary that condenses the transcript into a more manageable form. For this example, we will create these summaries using the widely used `gpt-3.5-turbo` model.

To [create an API key](https://platform.openai.com/account/api-keys), you must have an OpenAI account. You will be given some free usage as a new user to try out the API.

```python
import openai
openai.api_key = "<YOUR_OPENAI_API_KEY>"

def generate_summary(transcript: str) -> str:
    # Generate a summary of the transcript using OpenAI's gpt-3.5-turbo model.
    resp = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": f'Summarize this: {transcript}'},
        ]
    )
    return resp['choices'][0]['message']['content']

def main():
    transcript = transcribe('audio/bFIVYRfyb3E.m4a')
    summary = generate_summary(transcript)
    print(summary)
```

Although there may be variations in the outcomes, the following is an illustration of what to anticipate:

<details data-node-type="hn-details-summary"><summary>Summary</summary><div data-type="detailsContent">The passage describes an imaginary scenario in which the reader has lived every single human life that has ever existed, strung together for almost 4 trillion years. The vast majority of these lives are ordinary, consisting of everyday tasks like eating, working, and worrying. However, some lives are significant and shape the trajectory of human history. The reader's actions in their current life have a greater impact than those in their past lives, due to advances in technology and globalization. The passage encourages the reader to consider how they can work towards a better future for all their future lives.</div></details>

Have fun! To customize the answer to your objectives, you can adjust this in a variety of ways.

#### **Optional: Scale with Replicate ✌🏻**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684578620591/fad314ec-0afc-492f-844d-6423f2c2e10b.jpeg align="center")

We can run open-source models in the cloud thanks to Replicate. This might be a priceless tool for expanding your application, depending on your use case.

Create an account with Replicate to get an API token if you want to utilise it. We install the Replicate client using pip in order to use it in our code:

```python
pip install replicate
```

Now that Whisper through Replicate is enabled, we can adjust the transcribe code above to take this into consideration instead of only using the local CPU:

```python
def transcribe(file_path: str, use_replicate: bool = False) -> str:
    if use_replicate:
        client = replicate.Client(api_token='xxxxx')
        transcription = client.run(        'openai/whisper:30414ee7c4fffc37e260fcab7842b5be470b9b840f2b608f5baa9bbef9a259ed',
            input={'audio': open(file_path, 'rb')}, language='en', model='base'
        )['transcription']
    else:
        transcription = whisper_model.transcribe(file_path, fp16=False)['text']

    return transcription
```

#### **Conclusion 💭**

Whisper is a strong tool for creating transcribers that can effectively glean insights from audio and video sources. Whisper can help you optimize your workflow and discover fresh insights from your content, whether you’re a content creator trying to reuse your video content, a researcher analysing data from video interviews, or anybody else who deals with spoken data.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684578622055/82fd3fdc-fe9f-40bd-91a3-8af1477e6e3f.jpeg align="center")

Tell me what you believe! 🤔 Enjoy this post? 😃 Hungry for more? ✅

Don’t miss out by subscribing for more quality content delivered right to your inbox!

#### **Connect with Me on Social Media**

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)