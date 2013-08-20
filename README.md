XPathMagic
-------
>A chrome plugin to get simpler XPath of elemetns for using in independent html extractors.

##Prototype

### Single mode

When working in single mode, XPathMagic will try to extract XPath of selected element E in algorithm below:

#### *Algorithm I*

1. If the element has attribute ID, generate a XPath segment as tag[@id="xxx"]
2. Apply the XPath to whole html, if only E is selected, return the XPath as result, otherwise go to step 3.
3. Change attribute to 'class' and retry step 1-2.
4. If step 3 missed, go to the parent element of current and retry 1-3. The parent 's XPath is added before.
5. If root element (/html) is processed but there are still more than one reuslt, choose the lowest element with the same number of result. 

	e.g. /html/body/div[@class="a"] will be converted to //div[@class="a"]

![
image](https://raw.github.com/code4craft/xpathmagic/master/images/single.png)

### Compare mode

Sometimes the attributes of elements is relevant to the data of page. 

For example, &lt;div id="OSChina_News_43391"&gt; in page [http://www.oschina.net/news/43391/encryption-is-less-secure-than-we-thought](http://www.oschina.net/news/43391/encryption-is-less-secure-than-we-thought) uses the news id as a part of element id. In this page, although we extract the correct XPath //div[@id="OSChina_News_43391"]，it will not work in other pages.

So users can add another different page for extracting. This two pages are in a same kind but with diffent content.

When select element in the left page, the XPath will be extracted by *Algorithm I*. Then it will try to select elements in the right page. If matched, hightlight them and print answer. If not matched, consider the result as FAILURE and do step 4 in *Algorithm I*.

![image](https://raw.github.com/code4craft/xpathmagic/master/images/compare.png)

##License

Mit License