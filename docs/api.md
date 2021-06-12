## parse API
入力文字列からノードツリーを生成します。  
全てのMFM構文を利用可能です。  

例:  
```ts
const nodes = mfm.parse('hello [tada world]');
console.log(JSON.stringify(nodes));
// => "[{"type":"text","props":{"text":"hello "}},{"type":"fn","props":{"name":"tada","args":{}},"children":[{"type":"text","props":{"text":"world"}}]}]"
```

## parsePlain API
入力文字列からノードツリーを生成します。  
絵文字コードとUnicode絵文字を利用可能です。  

例:  
```ts
const nodes = mfm.parsePlain('Hello :surprised_ai:');
console.log(JSON.stringify(nodes));
// => "[{"type":"text","props":{"text":"Hello "}},{"type":"emojiCode","props":{"name":"surprised_ai"}}]"
```

## toString API
ノードツリーからMFM文字列を生成します。

例:  
```ts
const nodes = mfm.parse('hello [tada world]');
const output = mfm.toString(nodes);
console.log(output); // => "hello [tada world]"
```
※元の文字列とtoString APIで出力される文字列の同一性は保障されません。

## inspect API
ノードツリーの全ノードに指定された関数を適用します。  

例:  
```ts
mfm.inspect(nodes, node => {
  if (node.type == 'text') {
    node.props.text = node.props.text.replace(/Good morning/g, 'Hello');
  }
});
```

## extract API
ブール値を返す関数を渡してノードを抽出します。  
このAPIはノードツリーを再帰的に探索します。  

例:  
```ts
mfm.extract(nodes, (node) => {
  return (node.type === 'emojiCode');
});
```
