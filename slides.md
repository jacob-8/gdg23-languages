---
theme: seriph
background: /iguana-jump.jpg
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## 高雄 GDG DevFest 2023
drawings:
  persist: false
css: unocss
title: 使用 AI 學語言！
---

<br />
<br />
<br />
<br />
<br />
<br />
<br />

# 使用 AI 學語言！

大型語言模型、Google NLP 語法分析、機器翻譯

<div class="abs-br m-6 flex gap-2">
  <a href="http://github.com/jacob-8/gdg23-languages" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
大家好。我的主題是學語言。謝謝大家的興趣。現在我學中文。用過很多不同的方法：老師，課本，語言交換，台灣生活，舉辦活動，讀書，看電影，給演講，等，等。都有好處，壞處。關於學新的語言，最大的挑戰是了解這麼多的詞彙。

目前我了解兩千字，和七八千左右的詞。你們呢？三到五千字(漢字)，可能更多。兩萬到五萬詞彙（要看每一個人）。如果我們一起聊天呢，你一定會提到一些東西，事情，情況，我聽不懂。

所以學新的語言很難。學語言好像跳過很大的山谷。沒有橋。只有血、汗和淚。每天認真學習。但是我們有一些新的 AI 技術可以幫助我們跳過這麼大的山谷。今天我要分享如何使用大型語言模型 、Google 自然語言處理的語法分析和機器翻譯來快速學習語言。
-->

---
layout: image-right
image: /gao-tower.jpg
---

# 學習策略

- 有意義 (meaningful)
- 可理解 (comprehensible)

<img class="mt-6 w-29vw" src="/gao-letter.jpeg" />

<!--
為了用好AI，我們必須有一個學習策略。

我最喜歡的語言學習建議是 Steven Krashen 的建議：他說你需要很多有意義的、可理解的輸入。 為什麼我很喜歡這個建議？ 因為這種類型的輸入：

- 讓我專注中文（不要分心，專心）
- 給我能量和動力，可以花很多時間學習中文

我知道－跟朋友、真的人的對話是最有意義的輸入。 但是有時候你的朋友很忙，有時候你很累，有時候你的對方說得太快。 那麼，自己找到有意義、可理解的輸入的最好的方法是什麼？

高 Source: https://victor-seet.com/cliftonstrengths-blog/interpreting-emotions-using-chinese-language
-->

---
layout: image-right
image: /love-river.jpg
---

# 有意義的輸入

- 旅行
- 文化
- 自然
- 世界新聞
- AI
- 語言學習
- 科學（抱括電腦的）
- 歷史
- 小說

<!-- 首先，你需要找到有趣的內容。對我來說，最有趣的內容是母語人觀看的內容。真的生活，正常的內容，比如說： 

<< read list...

很幸運，Youtube 有很多真實的內容，還有字幕。
-->

---
layout: image-right
image: /riding-lamb.jpg
---

# 可理解的輸入

<v-clicks>

<img class="my-4 w-224px" src="/lambs.gif" />

- 大型語言模型
- Google 翻譯
- Google 自然語言處理: 語法分析

</v-clicks>

<!--
但是「可理解」嗎？這是一個問題，正常的華人說得很快。速度非常快。而且用非常描述性的詞語和文化概念。我不能完全理解。*我就像這些孩子一樣。 聽的時候我很努力，但很快就累了，跌倒了。然後休息。 

我需要的是一位導師，朋友，在我的語言學習中陪伴我左右。老師們的時間有限。朋友們的時間有限。 我所說的是一個每天每個小時的夥伴。只要我有時間就可以一起學習。

讓我們看看怎麼使用三種不同的 AI 來創建我們的個人語言導師。

<< read list*
-->

---
layout: image-right
image: /riding-lamb.jpg
---

# 步驟

- 選擇影片
- 取得字幕
- 總結內容 (**大型語言模型**) 
- **分析**內容+總結
- **翻譯**內容+總結

<!-- 簡單來說，有五個步驟 (read...)

讓我們觀看演示，然後我會解釋每個步驟。 -->

---

# 演示

<!-- Add video here -->

---

# 大型語言模型:總結內容

- 取得API金鑰: https://platform.openai.com/api-keys
- 添加串流服務器 endpoint
  ```ts {1,3,18|18-19}
  export const POST: RequestHandler = async ({ request }) => {
    const { captions } = await request.json()
    const completion = await openai.createChatCompletion({
      model: 'gpt-4-turbo',
      messages: [
          { role: 'system', content: system_message },
          { role: 'user', content: generate_user_prompt(captions) },
        ],
      max_tokens: 1000,
      temperature: 0,
    })
    const { choices: [{ message }] } = completion.data
    return json(message)
  }
  ```
- 在前端顯示摘要

<!-- Show summary screenshot first? 

選擇影片，還有取得字幕不是特別的, 你可以查看我的代碼。我們看一看 AI 的第一步。

觀看之前，我想要快速得預習我快要觀看的內容。 我可以把字幕送給 GPT4-turbo，說請給我整個影片的摘要。 當然，你可以使用任何語言模型。

這些是用 GPT4-turbo 的基本步驟：(read*) 

這是代碼的概念。全部的代碼是開源的。興趣的話，你可以自己更深入地研究。
-->

---

# Google 自然語言處理: 語法分析

## 斷詞問題: 
- 我**個人**認為
- **十個**人認為

## 解決方法:
- 取得API金鑰: TODO...
- 添加服務器 endpoint
  ```ts {1,3,18|18-19}
  export const POST: RequestHandler = async ({ request }) => {
    const { content } = await request.json()
    const response = fetch('') // TODO
    const { messages } = response.json()
    return json(messages)
  }
  ```
- 在前端顯示摘要

<!--
總結很棒，但我需要更多幫助。 這裡有一些字我不明白。 我想要一些自動字典和發音幫助顯示。但是中文沒有空格！怎麼自動地查字典？  這是一個斷詞問題。 之前我用過一個 package 叫 jieba-wasm ，效果還可以，但會出錯。 

我想要更好的方法，因為我想在學習中與我的導師快速討論新的詞彙。如果斷詞錯誤，這會變得很困難。 為此，我會使用 Google 語法分析來查找斷詞。這樣會幫助我我了解每個單字是什麼。
-->


--- 

# Google 翻譯

Show GIF of Showing/hiding translated portions as I study, just when I need them.

Lastly, the most foundational part of this tool is the use of automatic translations to help bring clarity when I am confused by a new word or complex sentence. Yes, you thought when I said using AI I would focus on the new language models. We need them, and they're helpful, but let's not forgot to use the existing AI technology that's already here. It's fast and cheap! The Google Translate API is a similar setup process to the 語法分析 and is totally worth it as it's only $1 per 五萬 characters with the first 五十萬免費的.

I use Google Translate to bring each sentence into English. This is key to making our desired content, comprehensible. I start in Chinese but if I don't understand and get confused, it's just a click away to be back in the loop. Confusion makes the brain tired and I want to make the language learning process take as little energy as possible so I can spend more energy learning.

Now everything out of language model and everything in our YouTube video will be automatically translated. But we'll put it out of sight so that we only look at it when needed. I don't want to just read English.

A key aspect of language learning is the **ability to notice**. I need to take note of new words and grammar patterns and how they are used in speech. This is why meaningful and comprehensive is important. If it's meaningful, I will be very interested in a particular sentence's meaning and I will want to take notice. But this only works if it's comprehensible. Sometimes the context of the movie will make the meaning clear. When it doesn't we can then lean on a translation.

Our goal in using AI is to enlarge the amount of natural and real language (not AI generated language) that we can consume in a day. We only have so much energy each day. There are two guys named John and Ash that run a Chinese learning business called Outlier Linguistics. I admire them and have used a lot of their resources to learn Chinese. But John gave some advice once that I disagree with. He talked about how in one of his Chinese classes, the professor would give a dialogue which had some new words. Their assignment would be to listen to the dialogue over and over and over until they could understand the meaning of the new words. They shouldn't look at the glossary, or at least they should try many times before looking at the glossary. I disagree with this advice. If you have a 6 minute dialogue and you listen through it multiple times, then listen through each sentence 5 or 6 times to try to understand and then you finally look at the glossary and then listen back through. The amount of time that would take could be an hour, hour and a half. It depends on the difficulty. While I think there is value in listening to something once, trying your best to understand it without looking at any translations, I think you shouldn't let yourself stay puzzling very long. A little puzzle is good. A lot will just make you tired and lose interest. We can use Google Translate to avoid the tired and losing interest part.

Let me say it another way: the first time a child learns the word shoe, the parent doesn't say "shoe" in a sentence and then ask the child to guess what it means. No, they put the shoe on the child's foot and point to it saying "shoe". They give a "translation" using a real world object. That's what the movie is for. It's goal is give picture translations to us. But sometimes speech is abstract and complex and can't always be pictured. The good news is that I've already grown up in English. I already understand many abstract concepts about life. I can use that pre-existing knowledge through a 1 second glance at an English translation and keep moving on my way.

So an English translation is available to help me regain comprehension whenever I lose focus. It's like this: horse-clips

--- 

# Google 翻譯: 安裝

- 取得API金鑰: TODO...
- 添加服務器 endpoint
  ```ts {1,3,18|18-19}
  export const POST: RequestHandler = async ({ request }) => {
    const { content } = await request.json()
    const response = fetch('') // TODO
    const { messages } = response.json()
    return json(messages)
  }
  ```
- 在前端顯示摘要

---

## Bonus: Explain word in context

Now I'm cruising, I started with a summary, I have my word breaks, I have my translations, and my dictionary help when I need it. Pretty cool. But let's not stop here. Not that I have all this analyzed data, my language model becomes even more useful. I can click on a word to get an explanation of the word's meaning in the context of the video.

## Bonus: Ask about something in the video

Another thing we can do with our language model is to ask a question at any point in the conversation to have a discussion about something. We can include the video summmary and the last few sentences of the clip for context and ask what the word means.


---
layout: iframe-right
url: https://tutor.polylingual.dev/zh-TW
---

# 現場演示

...

---

# 學英文

<!-- 
This has all been about studying Chinese which most of you don't need help with. Instead of learning Chinese with AI's help, you'd like to learn English with AI's help. Obviously with English you don't need the word breaks, but there are other aspects of Syntax analysis that you could find very helpful. And the conversational and translation pieces apply perfectly. In fact, there's more transcribed English content on YouTube than there is Chinese content. I'm currently working on making it go the other direction to allow you to watch English videos with help. If you're interested in working together with me to add support for learning English as a Chinese speaker, please let me know and we can work together (in Chinese). Some parts of the service will be free, like the video playing and dictionary lookups. Google Translate and syntax analysis will be free as long as I stay under the free tier. After that I'll have to pass on API costs to users but they're pretty cheap. If you don't want to pay, it's open source and if you help work on it, it'd be pretty easy for you to spin up your own copy and use your own API keys with free tiers. The only thing that will cost for sure, regardless is the conversational AI unless you use a local model. You could help me get that working too. That'd be cool. Anyhow, here's a QR code for our Facebook group and you can just contact me through Facebook or chat afterwards to get connected. Our first working session will be _________. If you can't make that time then just send me a message and we'll see if we can work something else out.
 -->

---

# 有問題嗎

- Slides: http://github.com/jacob-8/gdg23-languages
- Code: http://github.com/jacob-8/polylingual.dev
- [了解 JavaScript 高雄社團](https://www.facebook.com/groups/liaojiejavascript) 
  <img my-2 w-270px border="rounded" src="/facebook-qr.png">
- [@jacobbowdoin](https://twitter.com/jacobbowdoin)

<!--
I've showed some pseudo-code throughout the presentation, but you can go to github.com/jacob-8/polylingual.dev for the actual code to learn more. You can go to github.com/jacob-8/gdg23-languages for the slides.

有問題嗎, 掃描(sǎomiáo) QR code 進入我的 Facebook 社團。你會看到一個討論區，請把你的問題放在那邊(用中文)。如果我看不懂，我可以問我的學語言的夥伴。
-->
