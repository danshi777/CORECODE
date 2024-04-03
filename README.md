# CORECODE: A Common Sense Annotated Dialogue Dataset with Benchmark Tasks for Chinese Large Language Models

<p align="center">
    <a href="#introduction">Introduction</a> •
    <a href="#docs">Docs</a> •
    <a href="#data_format">Data Format for Each Task</a> •
    <a href="#citation">Citation</a> •
    <a href="#contact">Contact</a>
</p>

This is the repository for [CORECODE: A Common Sense Annotated Dialogue Dataset with Benchmark Tasks for Chinese Large Language Models](https://arxiv.org/abs/2312.12853) (AAAI 2024).

## Introduction

As an indispensable ingredient of intelligence, commonsense reasoning is crucial for large language models (LLMs) in real-world scenarios. In this paper, we propose CORECODE, a dataset that contains abundant commonsense knowledge manually annotated on dyadic dialogues, to evaluate the commonsense reasoning and commonsense conflict detection capabilities of Chinese LLMs. We categorize commonsense knowledge in everyday conversations into three dimensions: entity, event, and social interaction. For easy and consistent annotation, we standardize the form of commonsense knowledge annotation in open-domain dialogues as “domain: slot = value”. A total of 9 domains and 37 slots are defined to capture diverse commonsense knowledge. With these pre-defined domains and slots, we collect 76,787 commonsense knowledge annotations from 19,700 dialogues through crowdsourcing. To evaluate and enhance the commonsense reasoning capability for LLMs on the curated dataset, we establish a series of dialogue-level reasoning and detection tasks, including commonsense knowledge filling, commonsense knowledge generation, commonsense conflict phrase detection, domain identification, slot identification, and event causal inference. 

A wide variety of existing open-source Chinese LLMs are evaluated with these tasks on our dataset. Experimental results demonstrate that these models are not competent to predict CORECODE’s plentiful reasoning content.

## Docs

Below is the documentation tree, giving you an overview of the directory structure of each file:

```
+-- data
|   +-- easy
|   |   +-- generation
|   |   |   +-- dev
|   |   |   |   +--- Commonsense_Knowledge_Generation.jsonl
|   |   |   |   +--- Event_Causal_Inference--Clipped_Subsequent_Event_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Event_Cause_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Subsequent_Event_Inference.jsonl
|   |   |   +-- test
|   |   |   |   +--- Commonsense_Knowledge_Generation.jsonl
|   |   |   |   +--- Event_Causal_Inference--Clipped_Subsequent_Event_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Event_Cause_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Subsequent_Event_Inference.jsonl
|   |   |   +-- train
|   |   |   |   +--- Commonsense_Knowledge_Generation.jsonl
|   |   |   |   +--- Event_Causal_Inference--Clipped_Subsequent_Event_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Event_Cause_Inference.jsonl
|   |   |   |   +--- Event_Causal_Inference--Subsequent_Event_Inference.jsonl
|   |   +-- multiple_choice
|   |   |   +-- dev
|   |   |   |   +--- Commonsense_Knowledge_Filling.jsonl
|   |   |   |   +--- Domain_Identification.jsonl
|   |   |   |   +--- Slot_Identification.jsonl
|   |   |   +-- test
|   |   |   |   +--- Commonsense_Knowledge_Filling.jsonl
|   |   |   |   +--- Domain_Identification.jsonl
|   |   |   |   +--- Slot_Identification.jsonl
|   |   |   +-- train
|   |   |   |   +--- Commonsense_Knowledge_Filling.jsonl
|   |   |   |   +--- Domain_Identification.jsonl
|   |   |   |   +--- Slot_Identification.jsonl
|   |   +-- span_extraction
|   |   |   +-- dev
|   |   |   |   +--- Commonsense_Conflict_Phrase_Detection.jsonl
|   |   |   +-- test
|   |   |   |   +--- Commonsense_Conflict_Phrase_Detection.jsonl
|   |   |   +-- train
|   |   |   |   +--- Commonsense_Conflict_Phrase_Detection.jsonl
|   +-- hard
|   ... (similar structure as 'easy')
```

Note: 
+ In the **easy** set, we represent the subject and object of events using the speaker indicators “A” or “B” from the dialogue. 
+ In the **hard** set, “x” is uniformly employed to denote the subject of all events, while “y” is used to represent the predicate of all events, regardless of the dialogue participant to whom the event pertains.

## Data Format for Each Task

### Commonsense Knowledge Filling

```
{
  "id": 0,
  "dialogue": [
    "A: 嗨，你好。",
    "B: 你好啊。",
    "A: 你也在看这篇文章，对这方面的内容感兴趣嘛？",
    "B: 对啊，我特别喜欢看看电影，就看看这部新片子怎么样。",
    "A: 最近真在上映呢，看评价还不错，但是我很少看[MASK]。",
    "B: 我也是很少看科幻片，布拉德皮特是主演我很喜欢他的，影帝啊。",
    ...
    "B: 这部片子作者用片中人物的话表达了对肤色与人种，勇敢和孤独的见解。",
    "A: 哈哈哈哈，想想画面还挺和谐的，我还有事不说了啊。",
    "B: 嗯嗯，再见。"
  ],
  "question": "请根据对话内容，从a、b、c选项中选择对话中的[MASK]处应填入的选项。",
  "(a)": "科幻片",
  "(b)": "恐怖片",
  "(c)": "喜剧片",
  "answer": [
    "(a)",
    "科幻片"
  ]
}
```

### Commonsense Knowledge Generation

```
{
  "id": 173,
  "dialogue": [
    "A: 你好！",
    "B: 嗨！",
    "A: 你这是在看什么新闻啊？",
    "B: 有关乐视汽车莫干山土地被回收的以则新闻。",
    "A: 哦哦，这个不太了解，不懂汽车和土地有什么关系？",
    "B: 当然有关系了，你想啊，制造汽车不是得有场地吗？",
    "A: 对啊，当然得有场地，没有场地那这么制作啊！",
    "B: 对了，那土地被回收了厂房就没有了啊，没有厂房了那还这么制作汽车呢？",
    "A: 我懂了，那确实还是有很大的关系，看来乐视汽车只有重新找地块了。",
    "B: 对啊，但是对于他们公司来说也是很麻烦的一件事情啊，地块哪有那么好找。",
    "A: 所以说就相当于这个地块被回收了对他们公司来说就是大麻烦一个了！",
    "B: 没错，就是这个意思，找新的地块也不一定有那个区域的，那么合适的。",
    ...
  ],
  "question": "请根据对话内容，直接回答下面问题的答案，不要重述问题或解释原因：事件“乐视汽车莫干山土地被回收”的后续事件是什么？",
  "answer": "乐视汽车需要重新找地块"
}
```

### Commonsense Conflict Phrase Detection

```
{
  "id": 18,
  "dialogue": [
    "A: 嗨，你好啊。",
    "B: 嗨喽，你好。怎么啦？有什么事情吗？",
    "A: 嘿嘿，没事，我看你在看什么视频呢？这么激烈的。",
    "B: 哈哈哈，失态了。我正在看赛车的比赛呢。",
    "A: 哇，怪不得这么激烈的样子呢，你很喜欢赛车吗？",
    "B: 嗯嗯，对啊，这赛车手超帅的！哈哈哈。",
    "A: 这个赛车是有什么音乐啊？",
    "B: 可多了啊，有勒芒24小时汽车拉力赛，有世界汽车拉力锦标赛等等的。",
    "A: 哇，这么多比赛的呢？我以前还真不知道。",
    ...
  ],
  "question": "请从对话中抽取出在常识上与对话上下文不符的文本。注意不要重述问题或解释原因，直接写出答案即可。",
  "answer": "音乐"
}
```

### Domain Identification

```
{
  "id": 0,
  "dialogue": [
    ...
    "A: 嗯嗯，还是有点可惜了呢，温格真的是不错，在22年的阿森纳执教生涯中他带领球队夺得3次英超冠军、7次足总杯冠军等荣誉，创造了英超跨赛季49场不败的记录。",
    "B: 我去，你这知道的很清楚啊！",
    "A: 必须的啊，老球迷呢！温格可是夺得足总杯次数最多的教练。",
    "B: 嗯嗯，当时温格表达了想要执教拜仁的愿景，拜仁非常欣赏温格在阿森纳取得的成绩，但他不是拜仁主帅的选择之一。”这也意味着拜仁换帅的大门已经向温格关闭。",
    "A: 嗯嗯，只能说很好的球队和很好的教练没有火花，这个谁也不怨。",
    ...
  ],
  "question": "请根据对话内容，从a、b、c等候选领域中选择下面两个短语之间的关系所属的领域。\n短语1: 温格  短语2: 教练",
  "(a)": "属性",
  "(b)": "比较",
  "(c)": "空间",
  "answer": [
    "(a)",
    "属性"
  ]
}
```

### Slot Identification

```
{
  "id": 0,
  "dialogue": [
    "A: 你好啊。",
    "B: 你好。",
    "A: 你也在关注国足的新闻啊？你喜欢足球吗？",
    ...
    "A: 最近归化那个球员据说因为之前受伤已经接近一年没打过正式比赛了。",
    "B: 哎，国足不知道在干什么，现在关于国足的比赛我都不想看了，感觉让人太失望了。",
    "A: 是啊，就感觉是一群人在上面锻炼身体，看体育竞技的快感都没有了。",
    "B: 可不是吗，好歹也是打对抗吗，最近几年国足的表现简直就是自己砸自己招牌。",
    "A: 哎，不说了，我先走了哈。",
    "B: 嗯嗯，再见。"
  ],
  "question": "请根据对话内容，从a、b、c等选项中选择下面两个短语之间的关系。\n短语1：关于国足的比赛B一点都不想看  短语2：国足的比赛太让B失望了",
  "(a)": "前提条件",
  "(b)": "事件原因",
  "(c)": "情绪原因",
  "(d)": "时间原因",
  "(e)": "空间位置原因",
  "(f)": "后续事件",
  "(g)": "后续情绪反应",
  "(h)": "后续时间改变",
  "(i)": "后续空间位置改变",
  "(j)": "发生时间",
  "(k)": "开始时间",
  "(l)": "结束时间",
  "(m)": "持续时长",
  "(n)": "频率",
  "(o)": "发生位置",
  "answer": [
    "(b)",
    "事件原因"
  ]
}
```

### Event Causal Inference

#### Subtask 1: Event Cause Inference

```
{
  "id": 4192,
  "dialogue": [
    ...
    "B: 不过吧，这在我们中国应该是没有的吧，毕竟都是就近分配。",
    "A: 有啊，只不过都是在大山里面的孩子，而且他们还不是坐车是靠自己的走两三个小时到学校，在走回去。",
    "B: 这也太难了吧，两三个小时啊。这得多早起床，多晚到家哦。",
    "A: 可能她们也就习惯了吧，毕竟他们不读书就看没有出路。",
    "B: 这倒是，毕竟那里面太穷了。",
    "A: 我得去吃饭了，再见哈。",
    "B: 好的，再见！"
  ],
  "question": "请不要重述问题或解释原因，而是尽可能简短地回答下面的问题：根据对话内容可以看出，导致事件“大山里的孩子已经习惯了上学时间要三个小时”的原因是什么？",
  "answer": "大山里的孩子不读书就没有出路"
}
```

#### Subtask 2: Subsequent Event Inference

```
{
  "id": 2,
  "dialogue": [
    ...
    "B: 无人售货店，这么高级的东西嘛？我还是第一次听说。",
    "A: 你孤陋寡闻了吧，两年前就有了，现在移动支付这么发达，没有人照样收银交易。",
    "B: 那倒是确实，但万一有人故意买东西不给钱，他不就亏死了。",
    "A: 别人设计的时候早就想到了，必须要先注册会员留下身份信息，然后给了钱才可以出门。",
    "B: 这样哦，那应该万无一失了，毕竟不给钱不可能一直待在里面啊。",
    "A: 问题是有的人脑子就是不灵光，买很多东西却只象征性假装给一点点钱，然后就出门了。",
    "B: 居然还可以这样，简直是防不胜防，道高一尺，魔高一丈啊。",
    "A: 昨天我才看到北京有对情侣就是这样干的，可惜天网恢恢疏而不漏，直接通过人像对比一会儿就被抓了。",
    "B: 说的也是，现在到处都是监控，更何况注册时还留下了信息，想跑太难了。",
    "A: 要想人不知，除非己莫为。别人既然敢做无人售卖的生意，肯定留有后手啊。",
    "B: 看来待会儿我买东西要看清楚要付多少钱，不要给少了。",
    "A: 我朋友叫我了，我先去晨练了，拜拜。",
    "B: 拜拜。"
  ],
  "question": "请不要重述问题或解释原因，而是尽可能简短地回答下面的问题：根据对话内容可以看出，事件“北京有对情侣买东西不给够钱”导致的后续事件是什么？",
  "answer": "警察通过人像对比一会儿就把他们抓了"
}
```
#### Subtask 3: Clipped Subsequent Event Inference

```
{
  "id": 2,
  "dialogue": [
    ...
    "B: 无人售货店，这么高级的东西嘛？我还是第一次听说。",
    "A: 你孤陋寡闻了吧，两年前就有了，现在移动支付这么发达，没有人照样收银交易。",
    "B: 那倒是确实，但万一有人故意买东西不给钱，他不就亏死了。",
    "A: 别人设计的时候早就想到了，必须要先注册会员留下身份信息，然后给了钱才可以出门。",
    "B: 这样哦，那应该万无一失了，毕竟不给钱不可能一直待在里面啊。",
    "A: 问题是有的人脑子就是不灵光，买很多东西却只象征性假装给一点点钱，然后就出门了。",
    "B: 居然还可以这样，简直是防不胜防，道高一尺，魔高一丈啊。",
    "A: 昨天我才看到北京有对情侣就是这样干的，可惜天网恢恢疏而不漏，"
  ],
  "question": "请不要重述问题或解释原因，而是尽可能简短地回答下面的问题：根据对话上文可以推测出，事件“北京有对情侣买东西不给够钱”导致的后续事件是什么？",
  "answer": "警察通过人像对比一会儿就把他们抓了"
}
```

## Citation
```
@inproceedings{shi2024corecode,
  title={CORECODE: A Common Sense Annotated Dialogue Dataset with Benchmark Tasks for Chinese Large Language Models},
  author={Shi, Dan and You, Chaobin and Huang, Jiantao and Li, Taihao and Xiong, Deyi},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence},
  volume={38},
  number={17},
  pages={18952--18960},
  year={2024}
}
```

## Contact
Dan Shi: shidan@tju.edu.cn