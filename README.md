# SendSoapDocDirectly
Send a soap doc directly without waiting for it to go through the entire channel so you can get an immediate response.

```
<rule>
	<description>Send Soap Request Directly if Entitlement is Added</description>
	<conditions>
		<and>
			<if-class-name op="equal">User</if-class-name>
			<if-operation op="equal">modify</if-operation>
			<if-entitlement name="PenProPlus-Account" op="changing"/>
		</and>
	</conditions>
	<actions>
		<do-set-local-variable name="lvMessage" scope="policy">
			<arg-string>
				<token-text xml:space="preserve">&lt;modify></token-text>
				<token-text xml:space="preserve">&lt;xsd:APPNAME></token-text>
				<token-text xml:space="preserve">&lt;xsd:active></token-text>
				<token-local-variable name="lvActive"/>
				<token-text xml:space="preserve">&lt;/xsd:active></token-text>
				<token-text xml:space="preserve">&lt;/xsd:requestData></token-text>
				<token-text xml:space="preserve">&lt;/xsd:APPNAME></token-text>
				<token-text xml:space="preserve">&lt;/modify></token-text>
			</arg-string>
		</do-set-local-variable>
		<do-set-local-variable name="lvMessage" scope="policy">
			<arg-node-set>
				<token-xml-parse>
					<token-local-variable name="lvMessage"/>
				</token-xml-parse>
			</arg-node-set>
		</do-set-local-variable>
		<do-set-local-variable name="lvResult" scope="policy">
			<arg-node-set>
				<token-xpath expression="query:query($destQueryProcessor,$lvMessage)"/>
			</arg-node-set>
		</do-set-local-variable>
	</actions>
</rule>
```
