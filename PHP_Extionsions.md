**[Ctype PHP Extension]([PHP: Ctype - Manual](https://www.php.net/manual/en/book.ctype.php))** : This extension is enabled by default.

**[cURL PHP Extension]([PHP: cURL - Manual](https://www.php.net/manual/en/book.curl.php))**
```bash
apt install php-curl
```

**[DOM PHP Extension]([PHP: DOM - Manual](https://www.php.net/manual/en/book.dom.php))** : This extension is enabled by default.

**[Fileinfo PHP Extension]([PHP: Fileinfo - Manual](https://www.php.net/manual/en/book.fileinfo.php))** : This extension is enabled by default.

**[Filter PHP Extension]([PHP: Filter - Manual](https://www.php.net/manual/en/book.filter.php))** : This extension is enabled by default.

**[Hash PHP Extension]([PHP: Hash - Manual](https://www.php.net/manual/en/book.hash.php))** : The Hash extension is a core PHP extension, so it is always enabled.

**[Mbstring PHP Extension]([PHP: Installation - Manual](https://www.php.net/manual/en/mbstring.installation.php))** : `mbstring` is a non-default extension. This means it
 is not enabled by default. You must explicitly enable the module with the `configure` option.
```bash
apt install php-mbstring
```

**[OpenSSL PHP Extension]([PHP: OpenSSL - Manual](https://www.php.net/manual/en/book.openssl.php) )** : To use PHP's OpenSSL support you must also compile PHP **--with-openssl**.

**[PCRE PHP Extension]([PHP: PCRE - Manual](https://www.php.net/manual/en/book.pcre.php))** : The PCRE extension is a core PHP extension, so it is always enabled. By default, this extension is compiled using the bundled PCRE library.

**[PDO PHP Extension]([PHP: PDO - Manual](https://www.php.net/manual/en/book.pdo.php))** : enabled by php-mysql
```bash
apt install php-mysql
```

**[Session PHP Extension]([PHP: Session Extensions - Manual](https://www.php.net/manual/en/refs.basic.session.php))** : This extension is enabled by default.

**[Tokenizer PHP Extension]([PHP: Tokenizer - Manual](https://www.php.net/manual/en/book.tokenizer.php))** : This extension is enabled by default.

**[XML PHP Extension]([PHP: XML Parser - Manual](https://www.php.net/manual/en/book.xml.php))** : This extension is enabled by default. if missing you can install it using this command:
```bash
apt install php-xml
```

**[BCMath PHP Extension (optional) ]([PHP: BC Math - Manual](https://www.php.net/manual/en/book.bc.php))** : For arbitrary precision mathematics PHP offers BCMath which supports numbers of any size and precision up to `2147483647`decimal digits, if there is sufficient memory, represented as strings.
```bash
apt install php-bcmath
```

**[FastCGI Process Manager (FPM)]([PHP: FastCGI Process Manager (FPM) - Manual](https://www.php.net/manual/en/install.fpm.php))** :
```bash
apt install php-fpm
```

**[Zip PHP Extension]([PHP: Zip - Manual](https://www.php.net/manual/en/book.zip.php))** :
```bash
apt install php-zip
```
