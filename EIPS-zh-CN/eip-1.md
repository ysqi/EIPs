---
eip: 1
title: EIP 用途与指南
status: Living
type: Meta
author: Martin Becze <mb@ethereum.org>, Hudson Jameson <hudson@ethereum.org>, et al.
created: 2015-10-27
---

## 什么是以太坊改进提案？

EIP 代表以太坊改进提案（Ethereum Improvement Proposal 缩写）。 EIP 是向以太坊社区提供信息，或描述以太坊新功能，或其流程或环境的设计文档。 EIP 应提供功能的简明技术规范和基本原理。 EIP 创作者负责在社区内建立共识并记录不同意见。

## EIP 原理

我们打算将 EIP 作为主要机制，用于提出新功能、收集有关问题的社区技术输入，以及记录进入以太坊的设计决策。 由于 EIP 在版本化存储库中作为文本文件进行维护，因此其修订历史记录是功能提案的历史记录。

对于以太坊实施者来说，EIP 是跟踪其实施进度的便捷方式。 理想情况下，每个实施维护者都会列出他们已实施的 EIP。 这将使最终用户能够方便地了解某个实现或库的当下状态。

## EIP 类型

EIP 有 3 种类型：

- **标准类 EIP (Standards Track EIP)** 描述影响多数或全部以太坊实现的任何更改，例如网络协议的更改、块或交易有效性规则的更改、提议的应用程序标准/约定，或影响以太坊的应用程序交互的任何更改或添加。 标准类 EIP 由三部分组成 - 设计文档、实施和（如果有必要）对 [正式规范的更新](https://github.com/ethereum/yellowpaper)。 此外，标准类 EIP 可分为以下几类：
  - **核心 Core**: 需要共识分叉的改进(如 [EIP-5](./eip-5.md), [EIP-101](./eip-101.md)), 以及那些或许非共识关键但可能与 [“核心开发”讨论相关的变化](https://github.com/ethereum/pm)（如 [EIP-90]，矿工/节点策略更改[EIP-86](./eip-86.md)的2、3和4)。
  - **网络 Networking**: 包括对[devp2p][] ([EIP-8](./eip-8.md)) 和[以太坊轻客户端子协议][]的改进，以及对[whisper][]和[swarm][]网络协议规范的改进。
  - **接口 Interface **: 包括围绕客户端 [API/RPC](https://github.com/ethereum/execution-apis#README) 规格和标准的改进，还有某些语言级别的标准，如方法名 ([EIP-6](./eip-6.md)) 和 [合约 ABIs](https://docs.soliditylang.org/en/develop/abi-spec.html)。 标签“interface”与 [interfaces repo](https://github. com/ethereum/interfaces) 一致，在将 EIP 提交到 EIP 存储库之前，讨论应该主要发生在该存储库中。
  - **应用标准 ERC**：是应用程序级别的标准和约定，包括合约标准，如代币标准 ([ERC-20](./eip-20.md))、名称注册 ([ERC-137](./eip-137.md))、URI 方案、库/包格式和钱包格式等。

- **变化类 EIP ( Meta EIP )** 描述围绕以太坊的流程或提议对流程（或事件）进行更改。 流程 EIP 类似于标准跟踪 EIP，但流程 EIP 适用于以太坊协议之外的领域。 他们可能会提出一个实施方案，但不会针对以太坊代码库；他们通常需要社区达成共识；与信息 EIP 不同，它们不仅仅是建议，用户一般不能随意忽略它们。 这方面的提案包括程序、指南、决策过程的更改以及以太坊开发中使用的工具或环境的更改。 任何变化类 EIP 也会被视为流程 EIP。

- **信息类 EIP（ Informational EIP）** 描述以太坊的设计问题，或向以太坊社区提供一般的指南或资讯，而非提出新功能。 它不一定代表以太坊社区的共识或建议，所以用户和实施者可以自由的选择遵循或忽略信息类 EIP 所提出的建议。

强烈建议单个 EIP 只包含一个关键提案或新想法。 EIP 的重点越突出，就越能成功。 对单个客户端的更改不需要 EIP；影响多个客户端或供多个应用程序使用的标准定义的更改就需要 EIP。

EIP 必须满足某些最低标准。 它必须清楚和完整地描述提案的改进措施。 这种增强必须是一种净改进。 提案的实施（如果适用）必须是可靠的，并且不得使协议过度复杂化。

### 核心 EIP 的特殊要求

如果 **核心** EIP 提到或建议对 EVM (以太坊虚拟机) 进行更改，则应通过其助记符引用指令，并至少定义一次这些助记符的操作码。 首选方式如下：

```
REVERT (0xfe)
```

## EIP 工作流程

### Shepherding an EIP

EIP 流程的参与方是你、倡导者或* EIP 作者*、 [*EIP 编辑人*](#eip-editors)、以及[*Ethereum 核心开发者*](https://github.com/ethereum/pm)。

在开始编写正式的 EIP 之前，你应该仔细推敲你的想法。 首先询问以太坊社区这个想法是否是原创的，避免在基于先前研究而被拒绝的事情上浪费时间。 因此建议在[Ethereum Magicans论坛](https://ethereum-magicians.org/) 上弄一个主题来讨论它。

一旦该想法通过审核， 您的下一个责任将是(通过EIP) 向审阅员和所有感兴趣的各方介绍您的想法， 邀请编辑、开发人员和社区，在上述频道提供反馈。 你应评估对 EIP 的兴趣是否即和实施它所涉及的工作相称，也和有哪几方必须遵守它相适应。 例如，实施核心 EIP 所需的工作将比 ERC 大得多，并且 EIP 需要以太坊客户团队表现出足够的兴趣。 考虑社区负面反馈，这可能将会阻止您的 EIP 通过草图阶段。

### 核心 EIPs

对于核心EIPs，鉴于它们要求客户端实现才能被被认为 **Final** (见下文 “EIPs 流程”) ，你需要为客户端提供一个实现或者说服客户端实现你的 EIP。

让客户端实施者审阅你的 EIP 的最好方法是在 AllCoreDevs 的电话会议上介绍它。 你可以通过在 [AllCoreDevs 议程 GitHub Issue](https://github.com/ethereum/pm/issues) 上发布一条链接你的 EIP 的评论来请求这样做。

AllCoreDevs 电话是客户端实施者做三件事的一种方式。 第一，讨论 EIP 技术优点。 第二，衡量其他客户端将实施什么。 第三，协调网络升级的 EIP 实施。

这些通话通常会就应实施哪些 EIP 达成“大致的共识”。 这种 "大致的共识 "建立在这样的假设上：EIPs 没有争议到导致网络分裂的程度，且 EIPs 在技术上是合理的。

:warning: EIPs 流程和 AllCoreDevs 电话不是为了解决有争议的非技术问题，但由于缺乏其他方法来解决这些问题，最终往往被这些问题所纠缠。 这使得客户端实施者承担了尝试和衡量社区情绪的负担，这阻碍了 EIPs 和 AllCoreDevs 电话的技术协调功能。 如果你正在指导一个 EIP，你可以通过确保你的 EIP 的 [Ethereum Magicians 论坛 ](https://ethereum-magicians.org/)主题包括或链接到尽可能多的社区讨论，并确保各利益相关者得到足够的权利，从而使建立社区共识的过程更容易。

*简而言之，你作为倡导者的角色是使用下面描述的风格和格式来编写 EIP，在适当的论坛上引导讨论，并围绕这个想法建立社区共识。*

### EIP 流程

以下是所有轨道中所有 EIP 的标准化流程。

![EIP Status Diagram](../assets/eip-1/EIP-process-update.jpg)

**想法-Idea** - 一个预先起草的想法， 不在 EIP 资源库中跟踪。

**草稿-Draft** - EIP 进展中的第一个正式跟踪阶段。 当格式正确时，EIP 编辑者会将 EIP 合并到 EIP 资源库中。

**评审-Review** - EIP 作者将 EIP 标记为准备好并请求同行评审。

**终审- Last Call** - 这是 EIP 进入`Final`的终审窗口。 EIP编辑者将指定 `Last Call` 状态，并设定审查结束日期（`Last-call-deadline`），通常是14天后。

如果这段时间产生了必要的规范性修改，它将把 EIP 恢复为 `Review`。

**终稿-Final** - 该 EIP 代表了最终标准。 一个最终的 EIP 存在于最终状态，只应更新以纠正勘误和增加非规范性的澄清。

**停滞-Stagnant** - 任何处于`DRAFT` 或 `REVIEW` 或 `Last Call` 状态的EIP， 如果在 6 个月或更长时间内没有活动，将移至 `Stagnant`。 EIP 可由作者或编辑者通过将其移回`草案`或其早期状态，而从停滞中复活。 如果不复活，一个提案可能会永远停留在这个状态。
> *EIP作者会被通知其 EIP 状态的任何算法变化。*

**撤回-Withdrawn** - EIP 作者已撤回提案的 EIP。 这种状态具有终结性，不能再使用这个 EIP 编号复活。 如果这个想法在以后继续下去，它将被视为一个新的提案。

**活着-Living** - EIP 的特殊状态，适用于那些旨在持续更新而未达到最终状态的 EIP。 这包括最引入注目的 EIP-1。

## 哪些内容属于成功的 EIP ？

Each EIP should have the following parts:

- Preamble - RFC 822 style headers containing metadata about the EIP, including the EIP number, a short descriptive title (limited to a maximum of 44 characters), a description (limited to a maximum of 140 characters), and the author details. Irrespective of the category, the title and description should not include EIP number. See [below](./eip-1.md#eip-header-preamble) for details.
- Abstract - Abstract is a multi-sentence (short paragraph) technical summary. This should be a very terse and human-readable version of the specification section. Someone should be able to read only the abstract to get the gist of what this specification does.
- Motivation *(optional)* - A motivation section is critical for EIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the EIP solves. This section may be omitted if the motivation is evident.
- Specification - The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (besu, erigon, ethereumjs, go-ethereum, nethermind, or others).
- Rationale - The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale should discuss important objections or concerns raised during discussion around the EIP.
- Backwards Compatibility *(optional)* - All EIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their consequences. The EIP must explain how the author proposes to deal with these incompatibilities. This section may be omitted if the proposal does not introduce any backwards incompatibilities, but this section must be included if backward incompatibilities exist.
- Test Cases *(optional)* - Test cases for an implementation are mandatory for EIPs that are affecting consensus changes. Tests should either be inlined in the EIP as data (such as input/expected output pairs, or included in `../assets/eip-###/<filename>`. This section may be omitted for non-Core proposals.
- Reference Implementation *(optional)* - An optional section that contains a reference/example implementation that people can use to assist in understanding or implementing this specification. This section may be omitted for all EIPs.
- Security Considerations - All EIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the life-cycle of the proposal. E.g. include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. EIP submissions missing the "Security Considerations" section will be rejected. An EIP cannot proceed to status "Final" without a Security Considerations discussion deemed sufficient by the reviewers.
- Copyright Waiver - All EIPs must be in the public domain. The copyright waiver MUST link to the license file and use the following wording: `Copyright and related rights waived via [CC0](../LICENSE.md).`

## EIP Formats and Templates

EIPs should be written in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format. There is a [template](https://github.com/ethereum/EIPs/blob/master/eip-template.md) to follow.

## EIP Header Preamble

Each EIP must begin with an [RFC 822](https://www.ietf.org/rfc/rfc822.txt) style header preamble, preceded and followed by three hyphens (`---`). This header is also termed ["front matter" by Jekyll](https://jekyllrb.com/docs/front-matter/). The headers must appear in the following order.

`eip`: *EIP number* (this is determined by the EIP editor)

`title`: *The EIP title is a few words, not a complete sentence*

`description`: *Description is one full (short) sentence*

`author`: *The list of the author's or authors' name(s) and/or username(s), or name(s) and email(s). Details are below.*

`discussions-to`: *The url pointing to the official discussion thread*

`status`: *Draft, Review, Last Call, Final, Stagnant, Withdrawn, Living*

`last-call-deadline`: *The date last call period ends on* (Optional field, only needed when status is `Last Call`)

`type`: *One of `Standards Track`, `Meta`, or `Informational`*

`category`: *One of `Core`, `Networking`, `Interface`, or `ERC`* (Optional field, only needed for `Standards Track` EIPs)

`created`: *Date the EIP was created on*

`requires`: *EIP number(s)* (Optional field)

`withdrawal-reason`: *A sentence explaining why the EIP was withdrawn.* (Optional field, only needed when status is `Withdrawn`)

Headers that permit lists must separate elements with commas.

Headers requiring dates will always do so in the format of ISO 8601 (yyyy-mm-dd).

### `author` header

The `author` header lists the names, email addresses or usernames of the authors/owners of the EIP. Those who prefer anonymity may use a username only, or a first name and a username. The format of the `author` header value must be:

> Random J. User &lt;address@dom.ain&gt;

or

> Random J. User (@username)

if the email address or GitHub username is included, and

> Random J. User

if the email address is not given.

It is not possible to use both an email and a GitHub username at the same time. If important to include both, one could include their name twice, once with the GitHub username, and once with the email.

At least one author must use a GitHub username, in order to get notified on change requests and have the capability to approve or reject them.

### `discussions-to` header

While an EIP is a draft, a `discussions-to` header will indicate the URL where the EIP is being discussed.

The preferred discussion URL is a topic on [Ethereum Magicians](https://ethereum-magicians.org/). The URL cannot point to Github pull requests, any URL which is ephemeral, and any URL which can get locked over time (i.e. Reddit topics).

### `type` header

The `type` header specifies the type of EIP: Standards Track, Meta, or Informational. If the track is Standards please include the subcategory (core, networking, interface, or ERC).

### `category` header

The `category` header specifies the EIP's category. This is required for standards-track EIPs only.

### `created` header

The `created` header records the date that the EIP was assigned a number. Both headers should be in yyyy-mm-dd format, e.g. 2001-08-14.

### `requires` header

EIPs may have a `requires` header, indicating the EIP numbers that this EIP depends on. If such a dependency exists, this field is required.

A `requires` dependency is created when the current EIP cannot be understood or implemented without a concept or technical element from another EIP. Merely mentioning another EIP does not necessarily create such a dependency.

## Linking to External Resources

Other than the specific exceptions listed below, links to external resources **SHOULD NOT** be included. External resources may disappear, move, or change unexpectedly.

The process governing permitted external resources is described in [EIP-5757](./eip-5757.md).

### Consensus Layer Specifications

Links to the Ethereum Consensus Layer Specifications may be included using normal markdown syntax, such as:

```markdown
[Beacon Chain](https://github.com/ethereum/consensus-specs/blob/26695a9fdb747ecbe4f0bb9812fedbc402e5e18c/specs/sharding/beacon-chain.md)
```

Which renders to:

[Beacon Chain](https://github.com/ethereum/consensus-specs/blob/26695a9fdb747ecbe4f0bb9812fedbc402e5e18c/specs/sharding/beacon-chain.md)

Permitted Consensus Layer Specifications URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^https://github.com/ethereum/consensus-specs/blob/[0-9a-f]{40}/.*$
```

### Networking Specifications

Links to the Ethereum Networking Specifications may be included using normal markdown syntax, such as:

```markdown
[Ethereum Wire Protocol](https://github.com/ethereum/devp2p/blob/40ab248bf7e017e83cc9812a4e048446709623e8/caps/eth.md)
```

Which renders as:

[Ethereum Wire Protocol](https://github.com/ethereum/devp2p/blob/40ab248bf7e017e83cc9812a4e048446709623e8/caps/eth.md)

Permitted Networking Specifications URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^https://github.com/ethereum/devp2p/blob/[0-9a-f]{40}/.*$
```

### Digital Object Identifier System

Links qualified with a Digital Object Identifier (DOI) may be included using the following syntax:

````markdown
This is a sentence with a footnote.[^1]

[^1]:
    ```csl-json
    {
      "type": "article",
      "id": 1,
      "author": [
        {
          "family": "Jameson",
          "given": "Hudson"
        }
      ],
      "DOI": "00.0000/a00000-000-0000-y",
      "title": "An Interesting Article",
      "original-date": {
        "date-parts": [
          [2022, 12, 31]
        ]
      },
      "URL": "https://sly-hub.invalid/00.0000/a00000-000-0000-y",
      "custom": {
        "additional-urls": [
          "https://example.com/an-interesting-article.pdf"
        ]
      }
    }
    ```
````
Which renders to:
This is a sentence with a footnote.[^1]

See the [Citation Style Language Schema](https://resource.citationstyles.org/schema/v1.0/input/json/csl-data.json) for the supported fields. In addition to passing validation against that schema, references must include a DOI and at least one URL.

The top-level URL field must resolve to a copy of the referenced document which can be viewed at zero cost. Values under `additional-urls` must also resolve to a copy of the referenced document, but may charge a fee.

## Linking to other EIPs

References to other EIPs should follow the format `EIP-N` where `N` is the EIP number you are referring to.  Each EIP that is referenced in an EIP **MUST** be accompanied by a relative markdown link the first time it is referenced, and **MAY** be accompanied by a link on subsequent references.  The link **MUST** always be done via relative paths so that the links work in this GitHub repository, forks of this repository, the main EIPs site, mirrors of the main EIP site, etc.  For example, you would link to this EIP as `./eip-1.md`.

## Auxiliary Files

Images, diagrams and auxiliary files should be included in a subdirectory of the `assets` folder for that EIP as follows: `assets/eip-N` (where **N** is to be replaced with the EIP number). When linking to an image in the EIP, use relative links such as `../assets/eip-1/image.png`.

## Transferring EIP Ownership

It occasionally becomes necessary to transfer ownership of EIPs to a new champion. In general, we'd like to retain the original author as a co-author of the transferred EIP, but that's really up to the original author. A good reason to transfer ownership is because the original author no longer has the time or interest in updating it or following through with the EIP process, or has fallen off the face of the 'net (i.e. is unreachable or isn't responding to email). A bad reason to transfer ownership is because you don't agree with the direction of the EIP. We try to build consensus around an EIP, but if that's not possible, you can always submit a competing EIP.

If you are interested in assuming ownership of an EIP, send a message asking to take over, addressed to both the original author and the EIP editor. If the original author doesn't respond to the email in a timely manner, the EIP editor will make a unilateral decision (it's not like such decisions can't be reversed :)).

## EIP Editors

The current EIP editors are

- Alex Beregszaszi (@axic)
- Gavin John (@Pandapip1)
- Greg Colvin (@gcolvin)
- Matt Garnett (@lightclient)
- Sam Wilson (@SamWilsn)

Emeritus EIP editors are

- Casey Detrio (@cdetrio)
- Hudson Jameson (@Souptacular)
- Martin Becze (@wanderer)
- Micah Zoltu (@MicahZoltu)
- Nick Johnson (@arachnid)
- Nick Savers (@nicksavers)
- Vitalik Buterin (@vbuterin)

If you would like to become an EIP editor, please check [EIP-5069](./eip-5069.md).

## EIP Editor Responsibilities

For each new EIP that comes in, an editor does the following:

- Read the EIP to check if it is ready: sound and complete. The ideas must make technical sense, even if they don't seem likely to get to final status.
- The title should accurately describe the content.
- Check the EIP for language (spelling, grammar, sentence structure, etc.), markup (GitHub flavored Markdown), code style

If the EIP isn't ready, the editor will send it back to the author for revision, with specific instructions.

Once the EIP is ready for the repository, the EIP editor will:

- Assign an EIP number (generally the PR number, but the decision is with the editors)
- Merge the corresponding [pull request](https://github.com/ethereum/EIPs/pulls)
- Send a message back to the EIP author with the next step.

Many EIPs are written and maintained by developers with write access to the Ethereum codebase. The EIP editors monitor EIP changes, and correct any structure, grammar, spelling, or markup mistakes we see.

The editors don't pass judgment on EIPs. We merely do the administrative & editorial part.

## Style Guide

### Titles

The `title` field in the preamble:

- Should not include the word "standard" or any variation thereof; and
- Should not include the EIP's number.

### Descriptions

The `description` field in the preamble:

- Should not include the word "standard" or any variation thereof; and
- Should not include the EIP's number.

### EIP numbers

When referring to an EIP by number, it should be written in the hyphenated form `EIP-X` where `X` is the EIP's assigned number.

### RFC 2119 and RFC 8174

EIPs are encouraged to follow [RFC 2119](https://www.ietf.org/rfc/rfc2119.html) and [RFC 8174](https://www.ietf.org/rfc/rfc8174.html) for terminology and to insert the following at the beginning of the Specification section:

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

## History

This document was derived heavily from [Bitcoin's BIP-0001](https://github.com/bitcoin/bips) written by Amir Taaki which in turn was derived from [Python's PEP-0001](https://peps.python.org/). In many places text was simply copied and modified. Although the PEP-0001 text was written by Barry Warsaw, Jeremy Hylton, and David Goodger, they are not responsible for its use in the Ethereum Improvement Process, and should not be bothered with technical questions specific to Ethereum or the EIP. Please direct all comments to the EIP editors.

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
[^1]:
    ```csl-json
    {
      "type": "article",
      "id": 1,
      "author": [
        {
          "family": "Jameson",
          "given": "Hudson"
        }
      ],
      "DOI": "00.0000/a00000-000-0000-y",
      "title": "An Interesting Article",
      "original-date": {
        "date-parts": [
          [2022, 12, 31]
        ]
      },
      "URL": "https://sly-hub.invalid/00.0000/a00000-000-0000-y",
      "custom": {
        "additional-urls": [
          "https://example.com/an-interesting-article.pdf"
        ]
      }
    }
    ```

[devp2p]: https://github.com/ethereum/wiki/wiki/%C3%90%CE%9EVp2p-Wire-Protocol
[以太坊轻客户端子协议]: https://github.com/ethereum/wiki/wiki/Light-client-protocol
[whisper]: https://github.com/ethereum/go-ethereum/wiki/Whisper-Overview
[swarm]: https://github.com/ethereum/go-ethereum/pull/2959
