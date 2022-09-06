# investigation-of-Ref.State-Advanced

## Introduction
これらのコードは以下の調査のために作られました。

  ・複数のRef.State(**ここでは消費済みの2つのRef.State**)をトランザクションに含めた場合どうなるか？
  
  ・Notaryがエラーを出したRef.Stateのハッシュとインデックスを確認できるか？
また、これらのファイルはcorda training(https://github.com/sbir3japan/corda-dev-traning-sbir3japan.git )に追加することが前提になっています。

## Note 
**これらのコードはIOUIssueに焦点をおいているため、transferやsettleではRef.Stateは含まれません**

## Newly added files
### Put under "contracts\src\main\java\net\corda\training\states"
  AddressState.java: Ref.Stateに相当します
  
### Put under "contracts\src\main\java\net\corda\training\contracts"
  AddressContract.java: AddressStateのPublih(発行)とMove(更新)に関するコマンドを定義し、それらの関する制約を加えました。
  
### Put under "workflows\src\main\java\net\corda\training\flow"
  PublishFlow.java: AddressStateを発行するflow
    
  MoveFlow.java: AddressStateを更新するflow
    
  
## Changes to existing files
### Put under "contracts\src\main\java\net\corda\training\contracts"
  IOUContract.java: AddressStateとIOUStateのIssuerを突合させる制約を追加
    
### Put under "workflows\src\main\java\net\corda\training\flow"
  IOUIssueFlow.java:    AddressStateに関する処理を追加
  

## Procedure
以下はflowの実行手順になります。
  1. Run the nodes.
  2. Run PublishFlow.java
  3. Run MoveFlow.java  
      ※linearIdという引数にpublishされたAddressStateのLinearIdを指定してください。 
  4. Run PublishFlow.java.(※新たなaddressを指定することを推奨します)
  5. Run MoveFlow.java 
      ※linearIdという引数にpublishされたAddressStateのLinearIdを指定してください。
  6. Run IOUIssueFlow.java  
  7. Errored ref.State's hash and index will be display in the node terminal window.
