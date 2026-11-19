# AZ Permit Drill

A small, offline-friendly practice app for the Arizona MVD written (instruction permit) test. Open `index.html` in any browser. There's no build step and nothing to install.

亚利桑那 MVD 笔试（permit）刷题工具。用浏览器直接打开 `index.html` 就能用，不需要安装任何东西。

## Features / 功能

- **Scored rounds**: each round draws 30 questions from a bank of 199 and shuffles the answer order. Questions you haven't seen yet come first, so you work through the whole bank before anything repeats. 24 correct (80%, same as the real test) is a pass. Pass three rounds in a row and you're done.
- **Missed questions first**: questions you got wrong are mixed into the next round (up to 12 per round).
- **Missed-question book**: every question you've missed, sorted by how many times, with the correct answer and a short explanation.
- **Practice missed only**: a practice round made only of questions you haven't fixed yet. It doesn't count toward your scores or streak.
- **5 languages**: 中文, English, Español, Tiếng Việt, العربية (right-to-left). Switching language keeps your progress. All 199 questions are in Chinese; the other languages currently have the first 72.
- Progress is saved in your browser's `localStorage`. Nothing is sent anywhere.

---

- **正式轮**：每轮从 199 道题里抽 30 道，选项顺序也打乱。没见过的题优先出，整个题库轮完一遍才会重复。答对 24 道（80%，和真实考试一样）算达标，连续三轮达标就完成。
- **错题优先**：做错的题会混进下一轮（每轮最多 12 道）。
- **错题本**：所有做错过的题，按做错次数排序，附正确答案和解释。
- **只练错题**：只用还没改对的题组成一轮练习，不计入正式成绩和连续达标。
- **5 种语言**：中文、English、Español、Tiếng Việt、العربية（从右到左排版）。切换语言不影响进度。中文有全部 199 道，其他语言目前是前 72 道。
- 进度保存在浏览器的 `localStorage` 里，不会上传到任何地方。

## Why these languages / 为什么选这几种语言

After English, the languages most spoken at home in Arizona are Spanish (by far), Navajo, then Vietnamese, Arabic and Chinese at roughly 20,000 speakers each (U.S. Census data). Navajo isn't included because the MVD doesn't offer the written test in Navajo and a reliable traffic-law translation needs a native speaker. Contributions welcome.

除英语外，亚利桑那在家使用最多的语言依次是西班牙语、纳瓦霍语，以及越南语、阿拉伯语和中文（各约两万人）。纳瓦霍语没有收录，因为 MVD 不提供纳瓦霍语笔试，而且交通法规的准确翻译需要母语者。欢迎贡献。

## Project structure / 项目结构

```
index.html     page, styles and app logic
lang/zh.js     Chinese UI text + all 199 questions
lang/en.js     English (first 72 questions)
lang/es.js     Spanish
lang/vi.js     Vietnamese
lang/ar.js     Arabic
```

Each language file looks like this. Questions must stay in the **same order** in every file, because saved progress refers to questions by position. In each item the **first option is the correct one**; the app shuffles options at runtime. Items 63–65 ("All of the above") are kept in fixed order.

每个语言文件的格式如下。所有文件里的题目**顺序必须一致**，因为进度记录是按题目位置保存的。每道题的**第一个选项是正确答案**，程序运行时会自动打乱。第 63–65 题（"以上都是"）保持固定顺序。

```js
(window.AZQ = window.AZQ || {}).xx = {
  name: "Language name", dir: "ltr", htmlLang: "xx",
  ui: { /* interface text */ },
  items: [
    ["Question", ["Correct answer", "Wrong 1", "Wrong 2"], "Explanation"],
    ...
  ]
};
```

A language file may have fewer questions than `zh.js`; the app only draws from the questions that language has. To add a language, copy `lang/en.js`, translate it, add a `<script src="lang/xx.js">` line in `index.html`, and add the code to `LANG_ORDER`.

添加新语言：复制 `lang/en.js` 翻译，在 `index.html` 里加一行 `<script src="lang/xx.js">`，再把语言代码加进 `LANG_ORDER`。

## Disclaimer / 免责声明

Questions 1–72 are adapted from the three official ADOT/MVD driver license practice tests, with picture-based questions rewritten as text. Questions 73–199 were written for this project from the Arizona Driver License Manual. The answers and explanations were compiled for this project and are **not an official answer key**. The [Arizona Driver License Manual](https://azdot.gov/mvd) is the authority. Laws, fines and penalties can change.

This is an independent study tool and is not affiliated with or endorsed by the Arizona Department of Transportation.

第 1–72 题改编自 ADOT/MVD 官方的三套驾照练习题，看图题改写成了文字；第 73–199 题是本项目根据亚利桑那驾驶手册编写的。答案和解释由本项目整理，**不是官方答案键**，请以亚利桑那驾驶手册为准。法规、罚款和处罚可能会变。

本项目是个人学习工具，与亚利桑那州交通部无关，也未获其认可。

## License

Code: MIT (see `LICENSE`).
