# Tokenizer

Tokenizer的职责是是从字符流（a Reader）读取文本，处理文本生成一串分词（a TokenStream）。输入字符流中的字符在经Tokenizer处理过程中，会对字符或字符串进行特定处理，例如删除标点符号，替换字符或字符串，加入新的字符。所以生成分词中的文本可能和输入字符流中的文本不一致，并且可能有多个分词的位置相同或指向相同的偏移量。

>分词中除了包含文本信息，还包括位置等信息。

#### 1. Standard Tokenizer（solr.StandardTokenizerFactory）
以空格和标点符号为分隔符，将文本字段拆分成一串分词。在拆分过程中，分割符被丢弃，除了以下情况：   
1) 点（.）号后紧跟的字符不是空格，则点号以及其后的字符将会保留并作为分词的一部分。  
2) @符号被视为分隔符，所以电邮地址将不被当做一个分词，而是以@为分隔符拆开。  
>参数：  
>maxTokenLength，默认值255，超过maxTokenLength长度的字符将会被忽略。  

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
	</analyzer>

**IN:** "Please, email john.doe@foo.com by 03-09, re: m37-xq."  
**OUT:** "Please", "email", "john.doe", "foo.com", "by", "03", "09", "re", "m37", "xq"

#### 2. Classic Tokenizer（solr.ClassicTokenizerFactory）
以空格和标点符号为分隔符，将文本字段拆分成一串分词。在拆分过程中，分隔符被丢弃，除了以下情况：  
1) 点（.）号紧跟着的字符不是空格，则点号不被视为分隔符。  
2) 连字符（-）前后两侧紧跟着数字，此时连字符不给视为分隔符。  
3) 域名和电邮地址被保留为一个单独的分词，不拆分。  
>参数：  
>maxTokenLength，默认值255。

	<analyzer>
		<tokenizer class="solr.ClassicTokenizerFactory"/>
	</analyzer>

**IN:** "Please, email john.doe@foo.com by 03-09, re: m37-xq."  
**OUT:** "Please", "email", "john.doe@foo.com", "by", "03-09", "re", "m37-xq"

#### 3. Keyword Tokenizer（solr.KeywordTokenizerFactory）
将输入文本整体作为一个分词，不做拆解。  

	<analyzer>
		<tokenizer class="solr.KeywordTokenizerFactory"/>
	</analyzer>

**IN:** "Please, email john.doe@foo.com by 03-09, re: m37-xq."  
**OUT:** "Please, email john.doe@foo.com by 03-09, re: m37-xq."

#### 4. Letter Tokenizer（solr.LetterTokenizerFactory）
将连续字母作为分词，任何非字母字符都作为分隔符。任何非字母字符都被丢弃。  

	<analyzer>
		<tokenizer class="solr.LetterTokenizerFactory"/>
	</analyzer>

**IN:** "I can't."  
**OUT:** "I", "can", "t"

#### 5. Lower Case Tokenizer（solr.LowerCaseTokenizerFactory）
以非字母字符为分隔符，将输入流拆分，并将所有字母转成小写格式。空格以及非字母字符被丢弃。  

	<analyzer>
		<tokenizer class="solr.LowerCaseTokenizerFactory"/>
	</analyzer>

**IN:** "I just LOVE my iPhone!"  
**OUT:** "i", "just", "love", "my", "iphone"

#### 6. N-Gram Tokenizer（solr.NGramTokenizerFactory）
生成指定长度范围的n-gram分词。  
>参数：  
>1) minGramSize，默认值1，最小n-gram值。  
>2) maxGramSize，默认值2，最大n-gram值。

1) minGramSize，maxGramSize使用默认值

	<analyzer>
		<tokenizer class="solr.NGramTokenizerFactory"/>
	</analyzer>

**IN:** "hey man"  
**OUT:** "h", "e", "y", " ", "m", "a", "n", "he", "ey", "y ", " m", "ma", "an"

2) minGramSize=4，maxGramSize=5

	<analyzer>
		<tokenizer class="solr.NGramTokenizerFactory" minGramSize="4" maxGramSize="5"/>
	</analyzer>

**IN:** "bicycle"  
**OUT:** "bicy", "bicyc", "icyc", "icycl", "cycl", "cycle", "ycle"

#### 7. Edge N-Gram Tokenizer（solr.EdgeNGramTokenizerFactory）
生成指定长度范围的edge n-gram分词。
>参数：  
>1) minGramSize，默认值1。  
>2) maxGramSize，默认值1。  
>3) side，默认值front，计算n-grams方向，从前至后或者从后至前。  

1) minGramSize，maxGramSize使用默认值

	<analyzer>
		<tokenizer class="solr.EdgeNGramTokenizerFactory"/>
	</analyzer>

**IN:** "babaloo"  
**OUT:** "b"

2) minGramSize=2，maxGramSize=5，side=front

	<analyzer>
		<tokenizer class="solr.EdgeNGramTokenizerFactory" minGramSize="2" maxGramSize="5"/>
	</analyzer>

**IN:** "babaloo"  
**OUT:** "ba", "bab", "baba", "babal"

3) minGramSize=2， maxGramSize=5， side=back

	<analyzer>
		<tokenizer class="solr.EdgeNGramTokenizerFactory" minGramSize="2" maxGramSize="5" side="back"/>
	</analyzer>

**IN:** "babaloo"  
**OUT:** "oo", "loo", "aloo", "baloo"

#### 8. White Space Tokenizer（solr.WhitespaceTokenizerFactory）
以空格为分隔符拆分输入流生成分词。  

	<analyzer>
		<tokenizer class="solr.WhitespaceTokenizerFactory"/>
	</analyzer>

**IN:** "To be, or what?"  
**OUT:** "To", "be,", "or", "what?"
