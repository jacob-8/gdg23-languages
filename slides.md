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

# 使用 AI 學語言！

<div class="abs-br m-6 flex gap-2">
  <a href="http://github.com/jacob-8/gdg23-languages" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

<img class="w-full fixed left-0 top-0" src="/title.jpg" />

<!--
大家好。我的主題是如何用AI學語言。很開心大家的參與！我正在學習中文。用過很多不同的方法：老師、課本、語言交換、台灣生活、舉辦活動、讀書、看電影、演講、等等。都有好處和壞處。關於學新的語言，最大的挑戰是中文有這麼多的詞彙需要學習。

目前我了解兩千個漢字，和七八千個左右的詞。你們呢？三到五千個漢字，可能更多。兩萬到五萬個詞彙（要看每一個人）。如果我們一起聊天呢，你一定會提到一些東西、事情、情況、我聽不懂。
-->

---

<img class="w-full fixed left-0 top-0" src="/canyon.jpg" />

<!-- 所以學新的語言很難。學語言好像跳過很大的山谷。沒有橋。只有血、汗和淚。每天認真學習。但是我們有一些新的 AI 技術可以幫助我們跳過這麼大的山谷。今天我要分享如何使用大型語言模型 、Google 自然語言處理的語法分析和機器翻譯來快速學習語言。 -->

---
layout: image-right
image: /gao-tower.jpg
---

# 學習策略

- 有意義 (meaningful)
- 可理解 (comprehensible)

<img class="mt-6 w-29vw" src="/gao-letter.jpeg" />

<!--
為了好好用 AI，我們必須有一個學習策略。

我最喜歡的語言學習建議是 Steven Krashen 的建議：他說你需要很多有意義的、可理解的輸入。 為什麼我很喜歡這個建議？ 因為這種類型的輸入：

- 讓我專注中文（不要分心，要專心）
- 給我能量和動力，可以花很多時間學習中文

我知道－跟朋友、真的人的對話是最有意義的輸入。 但是有時候你的朋友很忙，有時候你很累，有時候對方說得太快。 你需要一個比較容易，自由的方法。怎麼找到？

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
- 學習語言
- 科學
- 歷史
- 小說

<!--
首先，你需要找到有趣的內容。對我來說，最有趣的內容是母語人士所觀看的內容。真的生活，正常的內容，比如說： 

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
- Google 自然語言處理: 語法分析
- Google 翻譯

</v-clicks>

<!--
但是「可理解」嗎？這是一個問題，正常的華人說得很快。速度非常快。而且用非常複雜的詞彙和文化概念。我不能完全理解。*我就像這些孩子一樣。 聽的時候我很努力，但很快就累了、跌倒了。然後必須休息。 

我需要的是一位導師、朋友，在我的語言學習中陪伴我。老師們的時間有限。朋友們的時間有限。 我所說的是一個每天每個小時的夥伴。只要我有時間就可以一起學習。

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

<!--
這個創建的過程有五個步驟 (read...)

讓我們先觀看一個演示，然後我會解釋每個步驟。
-->

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

<!--
Show summary screenshot first? 

第一步：選擇影片、第二步：取得的字幕不是難的，你可以自己查看我的代碼。我們看一看第三到第五步： AI 的部分。

我學中文的時候，在觀看一個影片之前，我想要快速得預習影片的內容。 我可以把字幕送給 GPT4-turbo，說：「請給我整個影片的摘要」。 

－－－work onmore：這些是用 GPT4-turbo 的基本步驟：(read*) 

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
layout: image-right
image: /love-river.jpg
---

# Google 翻譯

GIF of showing/hiding translated portions >>

<v-clicks>

<img class="my-4 w-full" src="/horse-jump.gif" />

</v-clicks>

<style>
  .grid-cols-2 {
    grid-template-columns: 3fr 2fr;
  }
</style>

<!--
最後，這工具最基本的部分是用自動翻譯來幫助我了解新單詞或複雜的句子。我知道新的AI功能很紅（大型語言模型），但我們不能忘記已有的AI技術。Google 翻譯非常快而且便宜！每五萬字符只是1塊美元，首五十萬字是免費的。

到這裡，我有英文，但我不要分心，一直讀英文。 只要我基本上理解了我正在觀看的內容，*我就像這個騎手一樣。 馬是影片，跨欄是每個新字，新語法。 如果我理解，那就好了，我可以繼續騎馬（繼續聽）。

但有時候， 我完全不明白一個，兩個，三個多的句子。
-->

---

# Google 翻譯

<img class="my-4 w-full" src="/horse-fall-and-drag-once.gif" />

<!--
就像我從馬背上摔下來一樣。馬繼續往前跑，而我只是被拖著跑。 我要繼續騎馬（了解內容的意思），不要被拖著。怎麼辦？
-->

---
layout: image-right
image: /love-river.jpg
---

# Google 翻譯

<!-- GIF of showing/hiding translated portions >> -->

<img v-click-hide class="my-4 w-200px" src="/get-back-on.gif" />
<img v-click class="my-4 w-full" src="/horse-jump.gif" />

<style>
  .grid-cols-2 {
    grid-template-columns: 3fr 2fr;
  }
</style>

<!--
我可以很快看著英文。好像騎馬者重新騎上馬並繼續騎馬。 我不花精力猜猜看。 我只是繼續騎。

with jump: 了解，不錯，喔。。。

另一方面，有時候你需要能夠在沒有幫助的情況，能夠自己重新騎上馬。 在生活對話中你需要能夠一直注意，一直猜猜看對方說什麼。 

但我從影片中學習的目標是在一天內聽很多中文。不一樣的情況。我要吃到飽而不累。
-->

---
background: /horse-running.gif
---

<img class="w-full" src="/horse-running.gif" />

<!--
換句話說，騎馬的時候，我要騎馬到非常遠的地方。 所以我必須留在馬背上。

另外好處是，如果我要看某部影片，我就看。 沒有什麼是太難的。
-->

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

# 另外一個功能: 根據上下文解釋一個單字

Image asking about a word >>

<!-- 關於這個AI導師的基本的功能，到這邊就好了。但我們不必就這邊停。 我們可以使用字幕和 GPT4-turbo 創建任何其他有用的功能。

我們可以點擊一個單字來問『在這個上下文，那個字有什麼意思？』 -->

---

# 另外一個功能: Ask about something in the video

Image asking a question >>

<!-- 或者我們可以在對話中隨時提出問題來討論某件事。 我們可以包含影片的摘要和最後幾句話以獲取上下文。 -->

---
layout: iframe-right
url: https://tutor.polylingual.dev/zh-TW
---

# 現場演示

...

---

- Slides: http://github.com/jacob-8/gdg23-languages
- Code: http://github.com/jacob-8/polylingual.dev
- Language tutor: https://tutor.polylingual.dev/zh-TW
- X: [@jacobbowdoin](https://twitter.com/jacobbowdoin)
- [了解 JavaScript 高雄社團](https://www.facebook.com/groups/liaojiejavascript) 
  <img my-2 w-260px border="rounded" src="/facebook-qr.png">

<!--
我今天只展示了簡單的代碼，因為使用 AI 最重要的事，你需要先了解用法概念。之後就可以寫代碼。正確概念比艱難。寫代碼比較容易。

如果你喜歡我分享的概念，請查看 github.com/jacob-8/polylingual.dev 以了解更多。 

我用字典、YouTube 和 Google 翻譯學習中文的經驗已經超過一年多了。 你今天看到的工具是重新寫代碼，以清理代碼並添加 Google 語法分析和大型語言模型。

我也知道我只討論了學中文，而且你們大多數人不需要學中文。 也許你對在 AI 的幫助下學英語更感興趣。 到目前，這個工具的用戶只是我、我太太和朋友們，但我正在擴展它，以及包括更多的語言，讓大家可以觀看英文的影片。

如果你有興趣跟我合作，為華人學英文提供支持，請告訴我，或者你可以在臉書上加入我的「了解 JavaScript 高雄社團」來與我聯繫。 我已經在那裡發布了今天的 PPT 和代碼的連結，還有我也會在那裡發布有關該工具的更新。

那，誰有問題？你可以直接問我。請你說簡單一點。如果你的問題比較複雜的話，請掃描這個 QR code，進入我的臉書社團。你會看到一個討論區，請把你的問題放在那邊。如果我看不懂，我可以問我學語言的導師。

開放的
開源的

Possible questions:

compound interest 我們使用的是複利原理。

Some parts of the service will be free, like the video playing and dictionary lookups. Google Translate and syntax analysis will be free as long as I stay under the free tier. After that I'll have to pass on API costs to users but they're pretty cheap. If you don't want to pay, it's open source and if you help work on it, it'd be pretty easy for you to spin up your own copy and use your own API keys with free tiers. The only thing that will cost for sure, regardless is the conversational AI unless you use a local model. You could help me get that working too. That'd be cool.
-->
