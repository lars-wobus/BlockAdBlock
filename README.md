Bypass BlockAdBlock (v3.2.1)
===========

No matter, if you are searching for a solution to bypass <i>AdBlock Detection</i> or to protect your website from visitors using <i>Adblockers</i>. The following description will give you some impressions on how easily someone can bypass <i>BlockAdBlock</i> in under 5 minutes per website.

## Prerequisites
- <i>Chrome</i> is already installed
- <i>AdBlock Plus</i> is already installed

## Initial Step
- Install [Resource Override](https://chrome.google.com/webstore/detail/resource-override/pkoacgokdfckfpndoffpifphamojphii?hl=en) or a similar browser plugin

## Steps Which Must Be Repeated For Each Website
- Start <i>Chrome</i> on your machine
- Open <i>Chrome DevTools</i>
- Select the <i>Network</i> tab
- Visit any website where you know that <i>AdBlock Plus</i> is being blocked
- Use the filter option to search for files called <i>blockadblock</i> or similar.
- Double click on that file to see the raw content of it<sup>1</sup>.
- Select all the content: <i>Ctrl + A</i>
- Copy all of it: <i>Ctrl + C</i>
- Click on the <i>Resource Override</i> Icon on the top right. Another browser tab will be opened!
- Click on the <i>Add Rule</i> button
- Select <i>Url &rarr; File</i>
- Click on the new <i>Edit File</i> button
- Paste all the content into the editor: <i>Ctrl + V</i>
- Click on the <i>Beautify JS</i> button on the top right, if the content is not already well-formatted
- Click on the <i>Find</i> button to the left or use <i>Ctrl + F</i> to open a search field
- Insert <i>detected</i>, <i>notDetected</i>, <i>this._var.event</i> or other strings to identify the following line<sup>2</sup><br />
 ```var fns = this._var.event[(detected===true?'detected':'notDetected')];```
- Replace the string 'detected' with 'notDetected' like the following<sup>3</sup><br />
 ```var fns = this._var.event[(detected===true?'notDetected':'notDetected')];```
- Click on <i>Save & Close</i>
- Go back to the website by selecting the previous browser tab.
- Right click on the file you previously doubled clicked
- Select <i>Copy > Copy link address</i>
- Select the <i>Resource Override</i> browser tab again
- Paste the URL into the text field left to the <i>Edit File</i> button
- Make sure the button right to the <i>Edit File</i> button is set to <i>on</i>
- Go back to the website by selecting the previous browser tab.
- Enable the <i>Disable cache</i> checkbox in <i>Chrome DevTools</i>
- Reload the website 

<sup>1</sup> You could also use this [modified content](https://github.com/lars-wobus/BlockAdBlock/blob/master/blockadblock.js), but keep in mind that websites have their own custom versions of <i>blockadblock.js</i> implmented. So it is always better to use their own content against them.
<br />
<sup>2</sup> Please note, that this line can slightly differ on each website. For instance, on another website it looked like this:<br />
```var e = this._var.event[!0 === t ? "detected" : "notDetected"];```
<br />
<sup>3</sup> Please note, that another line looks very similar. If you see <i>.push</i> at the end of the line, you might have found the wrong occurence. 

## Extra Step
- If the URL contains some strange characters, don't panic. It's properly a UUID (Universally Unique Identifier) which will be different on each visit. It's just another simple protection mechanism which can be bypassed. Just replace the ID with a single asterisks in the textfield within <i>Resource Override</i>. For instance<br />
<i>https://\<URL\>/blockadblock-93fc3395f09326b8a934f369fde11e9e.js</i><br />
will be replaced with<br />
<i>https://\<URL\>/blockadblock-*.js</i><br />
It means that we don't care so much about the correct spelling of the file.
	
## Remarks
Because your installing a plugin to manipulate incoming website content, you should be aware of some lacks of security. The browser plugin itself could contain malicious content. Furthermore anyone else having access to your machine and account can add additional files to manipulate web content. If you are afraid of those situations, you can still use another browser for important tasks, for instance to do online banking.
	
## How does it work.
When visiting a website, a bunch of files is downloaded. Some of them are Javascript files containing application logic. One of the Javascript files might be <i>blockadblock.js</i>. When Resource Override is enabled, it detects the occurrence of specified files and will replace their content with custom versions of it. Other javascript files do not notice the modification. They still calling functions defined in other files will now trigger modified versions of it. In the instant case AdBlock Plus is detected, but instead of calling the proper function, another existing function is called. It looks like AdBlock was not detected
	
## Lessons Learned
- Don't use <i>BlockAdBlock</i> in production.
- When delegating such tasks to contractors, check their outcome. Hopefully they do not implement BlockAdBlock. But I have already found <i>BlockAdBlock</i> inside of <i>CDNs</i> (Content Delivery Networks)
- Implement your personal <i>Adblock</i> protection instead or pay your web developers more money to implement some real protection!
- Don't lock your premium features, such as streaming without ads, behind <i>BlockAdBlock</i>
- Some websites restrict the use of robots, spiders and scammers in their terms of services. But configuring your own browser and sending a wrong signal back to their services is not always restricted. Good for us ;-)
