# explain-plan

Render a MarkLogic query plan for humans.

MarkLogic provides a way to get detailed information about how an expression will be evaluated against the configured indexes. [`xdmp:plan`](http://docs.marklogic.com/xdmp:plan?q=xdmp:plan) returns an XML report. The report is information dense, but difficult to decipher without deep knowledge of MarkLogic internals. 

## Objective
The goal of this project is make the critical information of how a query is executed more accessible to developers who are tuning search for performance and accuracy. 


```xml
<qry:query-plan xmlns:qry="http://marklogic.com/cts/query">
  <qry:info-trace>Analyzing path for search: fn:collection()/document
  </qry:info-trace>
  <qry:info-trace>Step 1 is searchable: fn:collection()</qry:info-trace>
  <qry:info-trace>Step 2 is searchable: document</qry:info-trace>
  <qry:info-trace>Path is fully searchable.</qry:info-trace>
  <qry:info-trace>Gathering constraints.</qry:info-trace>
  <qry:expansion-trace type="full" elapsed-time="PT0.000381S" text="cut?"
  counts="1">
    <qry:interval lowerbound="CUT" upperbound="C??"/>
    <qry:interval lowerbound="cUT" upperbound="c??"/>
    <qry:interval lowerbound="}UT" upperbound="???"/>
    <qry:expansion text="cute"/>
  </qry:expansion-trace>
  <qry:word-trace text="cute">
    <qry:key>16588943567160478160</qry:key>
  </qry:word-trace>
  <qry:info-trace>Search query contributed 1 constraint:
  cts:word-query("cut?", ("unstemmed","wildcarded","lang=en"), 1)
  </qry:info-trace>
  <qry:partial-plan>
    <qry:term-query weight="1">
      <qry:key>16588943567160478160</qry:key>
      <qry:annotation>word("cute")</qry:annotation>
    </qry:term-query>
  </qry:partial-plan>
  <qry:info-trace>Executing search.</qry:info-trace>
  <qry:final-plan>
    <qry:and-query>
      <qry:or-two-queries>
	<qry:term-query weight="0">
	  <qry:key>3998944933214536873</qry:key>
	  <qry:annotation>doc-root(element(document),doc-kind(document))
	</qry:annotation>
	</qry:term-query>
	<qry:term-query weight="0">
	  <qry:key>13616698357625443361</qry:key>
	  <qry:annotation>link-child(descendant(doc-root(element(document),
	     doc-kind(document)) ))
	</qry:annotation>
	</qry:term-query>
      </qry:or-two-queries>
      <qry:term-query weight="1">
	<qry:key>16588943567160478160</qry:key>
	<qry:annotation>word("cute")</qry:annotation>
      </qry:term-query>
    </qry:and-query>
  </qry:final-plan>
  <qry:info-trace>Selected 1 fragment to filter</qry:info-trace>
  <qry:result estimate="1"/>
</qry:query-plan>
```
