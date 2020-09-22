---
title: "blockchain"
author: "Marco Lee"
date: 2020-08-16T22:12:23+08:00
description: 關於 Blockchain 的研究心得
tags: ["Blockchain", "Ethereum"]
draft: true
---
這一篇要寫的是關於區塊鏈。

#### 一、使用Ganache、node和web3js與合約互動

以太坊虛擬機（Ethereum Virtual Machine，EVM）是建立在以太坊區塊鏈上去中心化的程式運行環境，其主要作用是處理以太坊系統內的智能合約。以太坊虛擬機是一個完全獨立的沙盒，合約程式碼可對外完全隔離在 EVM 內部運行。

#### 前言
EVM存在每一個以太坊節點中，負責執行存放在區塊中的 bytecode。編譯智能合約的原始碼，目的之一是形成可在 EVM 上執行的bytecode（binary code）。同時可以透過編譯取得智能合約的 ABI。部署智能合約的作業，實際上是透過一個交易（transaction）把 bytecode 儲存在區塊鏈上，並取得一個專屬此合約的地址。如果要呼叫這個智能合約，就要把訊息發送到這個合約地址。Ethereum 節點會根據接收到的訊息，選擇要執行合約中定義的功能。

#### 1. 建立專案開發環境

本研究在 MacOS 環境進行專案開發，採用以太坊開發工具 Truffle 套件中的 Ganache CLI 做為測試工具，此為開發以太坊私有鏈工具的命令列版本。Ganache CLI 模擬客戶端完整的行為，它包括所有主流的 RPC 函數功能，可以準確地模擬及運行。首先需為此專案建立專案資料夾，然後在專案資料夾中安裝 Ganache 及 web3js。操作如下：

```sh
$ cd InspecSheets
$ npm init --force		// 配置 package.json
$ npm install ganache-cli web3
```

啟動 Ganache CLI 的指令如下。啟動之後，Ganache CLI會自動建立 10 個測試用帳戶，並預設 100 個以太幣（ethers）如圖 3-2。操作如下：

```sh
$ ganache-cli
```