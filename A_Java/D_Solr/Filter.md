# Filter

Filter和Tokenizer一样都继承自org.apache.lucene.analysis.TokenStream。Filter读取一串分词流，并输出经过处理的一串分词流。
Filter读取和输出的都是TokenStream，因此可以配置一连串连续的Filters。每个Filter都按定义的顺序执行，处理前一个Filter处理过后的分词流。配置Filter的顺序非常重要，通常来说，最通用的Filter先执行，越是特殊的Filter执行顺序越靠后。

#### 1. Classic Filter（solr.ClassicFilterFactory）
读取Classic Tokenizer处理输出的分词流，删除缩写词中的点号（.），物主限定词中的"s"。  

	<analyzer>
		<tokenizer class="solr.ClassicTokenizerFactory"/>
		<filter class="solr.ClassicFilterFactory"/>
	</analyzer>

**IN:** "I.B.M. cat's can't"  
**Tokenizer to Filter:** "I.B.M", "cat's", "can't"  
**OUT:** "IBM", "cat", "can't"

#### 2. Edge N-Gram Filter（solr.EdgeNGramFilterFactory）
生成指定长度范围内的edge n-gram分词。  
>参数：  
>1) minGramSize，默认值1。  
>2) maxGramSize，默认值1。  

1) minGramSize，maxGramSize使用默认值

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.EdgeNGramFilterFactory"/>
	</analyzer>

**IN:** "four score and twenty"  
**Tokenizer to Filter:** "four", "score", "and", "twenty"  
**OUT:** "f", "s", "a", "t"

2) minGramSize=1，maxGramSize=4

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.EdgeNGramFilterFactory" minGramSize="1" maxGramSize="4"/>
	</analyzer>

**IN:** "four score"  
**Tokenizer to Filter:** "four", "score"  
**OUT:** "f", "fo", "fou", "four", "s", "sc", "sco", "scor"

3) minGramSize=4，maxGramSize=6

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.EdgeNGramFilterFactory" minGramSize="4" maxGramSize="6"/>
	</analyzer>

**IN:** "four score and twenty"  
**Tokenizer to Filter:** "four", "score", "and", "twenty"  
**OUT:** "four", "scor", "score", "and", "twen", "twent", "twenty"

#### 3. Lower Case Filter（solr.LowerCaseFilterFactory）
将分词中大写字母转换成小写字母。

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.LowerCaseFilterFactory"/>
	</analyzer>

**IN:** "Down With CamelCase"  
**Tokenizer to Filer:** "Down", "With", "CamelCase"  
**OUT:** "down", "with", "camelcase"

#### 4. N-Gram Filter（solr.NGramFilterFactory）
生成指定长度范围内的n-gram分词。  
>参数：  
>1) minGramSize，默认值1。  
>2) maxGramSize，默认值2。  

1) minGramSize，maxGramSize使用默认值

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.NGramFilterFactory"/>
	</analyzer>

**IN:** "four score"  
**Tokenizer to Filter:** "four", "score"  
**OUT:** "f", "o", "u", "fo", "ou", "ur", "s", "c", "o", "r", "e", "sc", "co", "or", "re"

2) minGramSize=1，maxGramSize=4

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.NGramFilterFactory" minGramSize="1" maxGramSize="4"/>
	</analyzer>

**IN:** "four score"  
**Tokenizer to Filter:** "four", "score"  
**OUT:** "f", "fo", "fou", "four", "s", "sc", "sco", "scor"

3) minGramSize=3，maxGramSize=5

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.NGramFilterFactory" minGramSize="3" maxGramSize="5"/>
	</analyzer>

**IN:** "four score"  
**Tokenizer to Filter:** "four", "score"  
**OUT:** "fou", "four", "our", "sco", "scor", "score", "cor", "core", "ore"

#### 5. Pattern Replace Filter（solr.PatternReplaceFilterFactory）
使用正则表达式匹配每个分词，如果匹配则用替代词替换匹配词。  
>参数：  
>1) pattern，必须指定，参照java.util.regex.Pattern。  
>2) replacement，必须指定，参照java.util.regex.Matcher。  
>3) replace，可选值"all"， "first"，默认"all"。

#### 6. Porter Stem Filter（solr.PorterStemFilterFactory）
使用Porter Steamming算法处理英文分词，生成分词词根。当设置Snowbll Porter Stemmer参数language为English时，两者生成的分词类似。但是处理速度Porter Stem Filter比Snowball快4倍。  

#### 7. Remove Duplicates Token FIlter（solr.RemoveDuplicatesTokenFIlterFactory）
删除分词流中重复的分词。文本值和位置值相同的分词被视为重复的分词。  

#### 8. Reversed Wildcard Filter（solr.ReveresedWildcardFilterFactory）
将带有星号（\*）前缀分词的字符反序输出，提高按前缀查询的速度。  

#### 9. Shingle Filter（solr.ShingleFilterFactory）
生成分词的n-grams（shingles），即将多个分词合并成一个分词。  
>参数：  
>1) minShingleSize：默认值2，每个shingle包含最少分词个数。  
>2) maxShingleSize：默认值2，每个shingle能包含最多分词个数。  
>3) outputUnigrams：可选值true/false，默认为true。如果为true，表示保留原始分词在原始位置上。  
>4) outputUnigramsIfNoShingles：默认为false。  
>5) tokenSeparator：默认值“ ”。用来连接相邻分词的分隔符。  

1) 参数取默认值

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.ShingleFilterFactory"/>
	</anlyzer>

**IN:** "To be, or what?"  
**Tokenizer to Filter:** "To"(1), "be"(2), "or"(3), "what"(4)  
**OUT:** "To"(1), "To be"(1), "be"(2), "be or"(2), "or"(3), "or what"(3), "what"(4)

2) maxShingleSize=4，outputUnigrams=false

	<analyzer>
		<tokenizer class="solr.StandardTokenizerFactory"/>
		<filter class="solr.ShingleFilterFactory" maxShingleSize="4" outputUnigrams="false"/>
	</analyzer>

**IN:** "To be, or not to be"  
**Tokenizer to Filter:** "To"(1), "be"(2), "or"(3), "not"(4), "to"(5), "be"(6)  
**OUT:** "To be"(1), "To be or"(1), "To be or not"(1), "be or"(2), "be or not"(2), "be or not to"(2), "or not"(3), "or not to"(3), "or not to be"(3), "not to"(4), "not to be"(4), "to be"(5)

#### 10. Stop Filter（solr.StopFilterFactory）

#### 11. Trim Filter（solr.TrimFilterFactory）
删除分词开头结尾处的空格。

	<analyzer>
		<tokenizer class="solr.PatternTokenizerFactory" pattern=","/>
		<filter class="solr.TrimFilterFactory"/>
	</analyzer>

**IN:** "one, two, three ,four"  
**Tokenizer to Filter:** "one", " two", "three ", "four"  
**OUT:** "one", "two", "three", "four"

#### 12. Word Delimiter Filter（solr.WordDelimiterFilterFactory）
