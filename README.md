# node-red-contrib-file-function

**This Node-RED node is just like the [core node "function"](http://nodered.org/docs/writing-functions.html), only that this node loads the script to be executed from an actual file on your drive.**

This may help you developing for Node RED. Instead of having to write your Javascript code in that small textfield in your browser you can use your favorite editor/IDE. The file will be read every time the node is called, so there's no need to redeploy or restart Node-RED.

The file path will be relative from the path set in _settings.userDir_, or if not set from the Node-RED install directory.

## Usage

Writing functions in this node works works just like functions in the the original function node (except that you write it in an actual file and no in an input field):

> The message is passed in as a JavaScript object called msg.
> 
> By convention it will have a `msg.payload` property containing the body of the message.
> 
> The function should return the messages it wants to pass on to the next nodes in the flow. It can return:
> 
> * a single message object - passed to nodes connected to the first output
> * an array of message objects - passed to nodes connected to the corresponding outputs
> 
> If any element of the array is itself an array of messages, multiple messages are sent to the corresponding output.
> 
> If null is returned, either by itself or as an element of the array, no message is passed on.
> 
> See the [online documentation](http://nodered.org/docs/writing-functions.html) for more help.


## Sample
Create a file called `sample-file-function.js` in your Node-RED root folder. Add the following content to that file:

```javascript
var reversedPayload = msg.payload.split("").reverse().join("");

return {
    payload: 'This is the input payload, but reversed: ' + reversedPayload
};
```

Import this flow (or add it manually by creating a simple [inject] > [file function] > [debug] flow yourself. Add the value `sample-file-function.js` to the _filename_ field in the _file function_ node):

```javascript
[{"id":"62efe026.9d102","type":"inject","name":"Inject","topic":"this is topic from the function","payload":"this data is feeded to the function","payloadType":"string","repeat":"","crontab":"","once":false,"x":303,"y":119,"z":"dd1ad5c3.22e528","wires":[["fd11ceda.02ee3"]]},{"id":"fd11ceda.02ee3","type":"file function","name":"","filename":"sample-file-function.js","outputs":"1","x":508,"y":119,"z":"dd1ad5c3.22e528","wires":[["7e85f5db.817a0c"]]},{"id":"7e85f5db.817a0c","type":"debug","name":"","active":true,"console":"false","complete":"true","x":723,"y":118,"z":"dd1ad5c3.22e528","wires":[]}]
```

Deploy the changes and click the inject node - check the output in the debug sidebar!
