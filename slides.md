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

目前我了解兩千個漢字，和七八千個左右的詞。你們呢？五到八千個漢字，可能更多。兩萬到五萬個詞彙（要看每一個人）。如果我們一起聊天呢，你一定會提到一些我聽不懂的東西、事情、情況。
-->

---

<img class="w-full fixed left-0 top-0" src="/canyon.jpg" />

<!--
所以學新的語言很難。學語言就像是要跳過很大的山谷。沒有橋。只有血、汗和淚。每天認真學習。但是我們有一些新的 AI 技術可以幫助我們跳過這麼大的山谷。今天我要分享如何使用大型語言模型 、Google 自然語言處理的語法分析和機器翻譯來快速學習語言。
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
為了好好用 AI，我們必須有一個學習策略。

我最喜歡的語言學習建議是 Steven Krashen 的建議：他說你需要很多有意義的、可理解的輸入。 為什麼我很喜歡這個建議？ 因為這種類型的輸入：

- 讓我專注中文（不會分心，可以更專心）
- 給我能量和動力，可以讓我有更多時間學習中文

(explain 高 picture)

我知道：跟朋友、真的人的對話是最有意義的輸入。 但是有時候你的朋友很忙，有時候你很累，有時候對方說得太快。 你需要一個比較容易，自由的方法。怎麼找到？

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
image: /process-overview.gif
---

# 步驟

- 選擇影片
- 取得字幕
- 摘要內容 (**大型語言模型**) 
- **分析**摘要+內容
- **翻譯**摘要+內容

<style>
  .grid-cols-2 {
    grid-template-columns: 2fr 3fr;
  }
</style>

<!--
這個創建的過程有五個步驟 (read...)

讓我們先觀看一個演示，然後我會解釋每個步驟。
-->

---

# 演示

<!-- Add video here -->

---

# 大型語言模型：摘要內容

- 取得API金鑰：https://platform.openai.com/api-keys
- 添加串流服務器 endpoint
  ```ts
  export const POST: RequestHandler = async ({ request }) => {
    const { model, messages } = await request.json()
    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${OPENAI_API_KEY}`,
      },
      body: JSON.stringify({
        model,
        messages,
        stream: true,
        temperature: 0,
      }),
    })
    return new Response(response.body, { headers: { 'Content-Type': 'text/event-stream;charset=utf-8' } })
  }
  ```
- 在前端顯示摘要

<!--
第一步：選擇影片、第二步：取得的字幕不是難的，你可以自己查看我的代碼。我們看一看第三到第五步： AI 的部分。

我學中文的時候，在觀看一個影片之前，我想要快速得預習影片的內容。 我可以把字幕送給 GPT3.5/4-turbo，說：「請給我整個影片的摘要」。 

基本的過程像這樣子：(read*) 

這是代碼的概念。全部的代碼是開源的。有興趣的話，你可以自己更深入地研究。
-->

---

# Google 自然語言處理: 語法分析

## 斷詞問題: 
- 我.**個人**.認為
- **十個**.人認為

<v-clicks>

<img class="my-4 w-full" src="/kaibi-not-analyzed.png" />

</v-clicks>

<!--
摘要很棒，但我需要更多幫助。 這部影片有一些字我不明白。 我想要一些字典提示。關於使用字典，中文的話要先斷詞，然後電腦可以自動給你一個解釋（因為中文沒有空格）。要怎麼解決呢？這是一個斷詞問題。 之前我用過一個 package 叫 jieba-wasm ，效果還可以，但有時候會出錯。

我想要更好的方法，因為我想在學習中與我的導師快速討論新的詞彙。如果斷詞錯誤，這會變得很困難。 為此，我會使用 Google 語法分析來查找斷詞。這樣會幫助我了解每個詞彙是什麼。

你可以看到分析之前...
-->

---

# Google 自然語言處理: 語法分析

## 斷詞問題: 
- 我.**個人**.認為
- **十個**.人認為

<img class="my-4 w-full" src="/kaibi-analyzed.png" />

<!--
...分析之後
-->

---

# Google 自然語言處理: 語法分析

- 取得API金鑰: https://cloud.google.com/natural-language
- 添加服務器 endpoint
  ```ts
  const languageServiceClient = new LanguageServiceClient({ credentials: CREDENTIALS, projectId: CREDENTIALS.project_id })
  
  export const POST: RequestHandler = async ({ request }) => {
    const { content, language } = await request.json()
    const [syntax] = await languageServiceClient.analyzeSyntax({
      document: {
        content,
        language, // 'en' or 'zh'
        type: 'PLAIN_TEXT',
      },
      encodingType: 'UTF8',
    })
    return json(syntax)
  }
  ```
- 在前端顯示分析

<!--
基本安裝的過程如下：

https://cloud.google.com/natural-language/docs/analyzing-syntax?hl=zh-cn
-->

---
layout: image-right
image: /show-hide-translations.gif
---

# Google 翻譯

<v-clicks>

<img class="my-4 w-full" src="/horse-jump.gif" />

</v-clicks>

<!-- <style>
  .grid-cols-2 {
    grid-template-columns: 3fr 2fr;
  }
</style> -->

<!--
最後，這工具最基本的部分是用自動翻譯來幫助我了解新單詞或複雜的句子。我知道新的AI功能很紅（大型語言模型），但我們不能忘記已有的AI技術。Google 翻譯非常快而且便宜！每五萬字符只是1塊美元，首五十萬字是免費的。

現在，我有英文，但我不要一直讀英文。 只要我基本上理解了我正在觀看的內容，*我就像這個騎手一樣。 馬是影片，跨欄是每個新字，新語法。 如果我理解，那就好了，我可以繼續騎馬（繼續聽）。

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
image: /show-hide-translations.gif
---

# Google 翻譯

<img class="my-4 w-300px" src="/get-back-on.gif" />

<!--
我可以很快看著英文。好像騎馬者重新騎上馬並繼續騎馬。 我不用花精力猜它的意思。 我只需要繼續騎（聽）。

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

- 取得API金鑰: https://cloud.google.com/translate
- 添加服務器 endpoint
```ts {all|4|5-11}
const translationClient = new TranslationServiceClient({ credentials: CREDENTIALS, projectId: CREDENTIALS.project_id })

export const POST: RequestHandler = async ({ request }) => {
  const { text, sourceLanguageCode, targetLanguageCode } = await request.json()
  const [response] = await translationClient.translateText({
    parent: `projects/${CREDENTIALS.project_id}/locations/global`,
    contents: [text],
    mimeType: 'text/plain',
    sourceLanguageCode,
    targetLanguageCode,
  })
  const translation = response.translations.map(t => t.translatedText).join('\n')
  return json(translation)
}
```
- 在前端顯示翻譯

<!--
基本安裝的過程跟語法分析很像：
-->

---

# 另外一個功能

- 根據上下文解釋一個單字
- 根據上下文提出問題
<!--
關於這個AI導師的基本的功能，到這裡應該就夠了。但我們不只是停留在這裡，我們還可以做得更好。我們可以使用字幕和 ChatGPT 創建任何其他有用的功能。

我們可以點擊一個詞彙來問『在這個上下文，這個詞彙有什麼意思呢？』

或者我們可以在對話中隨時提出問題來討論某件事。 我們可以包含影片的摘要和最後幾句話以獲取上下文。 -->

---
layout: iframe-right
url: https://tutor.polylingual.dev/zh-TW/shows
---

# 現場演示

<!--
簡單的解釋到這裡，現在我有現場演示。

http://localhost:5173/zh-TW/shows
https://tutor.polylingual.dev/zh-TW/shows
-->

---

- Slides: http://github.com/jacob-8/gdg23-languages
- Code: http://github.com/jacob-8/poly-tutor
- Language tutor: https://tutor.polylingual.dev/zh-TW
- X: [@jacobbowdoin](https://twitter.com/jacobbowdoin)
- [了解 JavaScript 高雄社團](https://www.facebook.com/groups/liaojiejavascript) 
  <img my-2 w-260px border="rounded" src="/facebook-qr.png">

<!--
我今天只展示了簡單的代碼，因為使用 AI 最重要的事，你需要先了解用法概念。之後就可以寫代碼。正確概念比艱難。寫代碼比較容易。

如果你喜歡我分享的概念，請查看以下的連結以了解更多。 

我用字典、YouTube 和 Google 翻譯學習中文的經驗已經超過一年多了。 你今天看到的工具是重新寫代碼，以清理代碼並添加 Google 語法分析和大型語言模型。

我也知道我只討論了學中文，而且你們大多數人不需要學中文。 也許你對在 AI 的幫助下學英語更感興趣。 到目前，這個工具的用戶只是我、我太太和一些朋友們，但我正在擴展它，以及包括更多的語言，讓大家可以觀看英文的影片。

如果你有興趣跟我合作，為華人學英文提供支持，請告訴我，或者你可以在臉書上加入我的「了解 JavaScript 高雄社團」來與我聯繫（請掃描這個 QR code）。 我已經在那裡發布了今天的 PPT 和代碼的連結，還有我也會在那裡發布有關該工具的更新。

那，大家有問題的話，你們可以發問。如果可以的話請說簡單一點。

Skip:
如果你的問題比較複雜的話，請掃描這個 QR code，進入我的臉書社團。你會看到一個討論區，請把你的問題放在那邊。如果我看不懂，我可以問我學語言的導師。


Possible questions:

compound interest 我們使用的是複利原理。

Some parts of the service will be free, like the video playing and dictionary lookups. Google Translate and syntax analysis will be free as long as I stay under the free tier. After that I'll have to pass on API costs to users but they're pretty cheap. If you don't want to pay, it's open source and if you help work on it, it'd be pretty easy for you to spin up your own copy and use your own API keys with free tiers. The only thing that will cost for sure, regardless is the conversational AI unless you use a local model. You could help me get that working too. That'd be cool.
-->
