# 6-7 Security filtering of read data



1. Purpose: At the time of depositing, I wanted to save it completely, and some dangerous grammar \(if any\) may be stored inherently. Therefore, some grammars that may harm the website must be filtered when reading data from the database.
2. The same must first enable the text filter:

   ```text
   $myts = MyTextSanitizer::getInstance();
   ```

3. According to the amount of data, it is divided into two categories, one is a large number of text types \(such as textarea large text boxes or fields in CKEditor editor\), and the other is general data, such as names, numbers... etc.
4. Render a lot of text:

   ```text
   $myts->displayTarea($text, $html=0, $smiley=1, $xcode=1, $image=1, $br=1);
   ```

   * \(1\) "$text" is the text to be presented after being processed.
   * \(2\) Whether "$html" allows the use of HTML syntax, please fill in 1 if it is created with a WYSIWYG editor.
   * \(3\) Whether "$smiley" should be converted into emoticons, the default is 1, which will convert symbols like :\) into pictures.
   * \(4\) Whether "$xcode" uses BBCode, such as: \[color=red\]text\[/color\].
   * \(5\) Whether "$image" allows images to be used in text. If it is 0, the picture will be displayed as a link.
   * \(6\) Whether "$br" should convert the "\n" line break into &lt;br&gt;, please set it to 0 if you use WYSIWYG editor .

5. Present general text:

   ```text
   $myts->htmlSpecialChars($text, $quote_style=ENT_QUOTES, $charset= null, $double_encode=true);
   ```

   * \(1\) "$text" is the text to be presented after being processed.
   * \(2\) The quotation mark mode to be handled by "$quote\_style", "ENT\_COMPAT" only handles double quotes; "ENT\_QUOTES" handles double quotes and single quotes \(default\); "ENT\_NOQUOTES" does not handle any quotes.
   * \(3\) The default encoding for "$charset" conversion, usually use the default value.
   * \(4\) "$double\_encode" is only valid after PHP 5.2.3. If set to false, the existing HTML entities will not be encoded.

