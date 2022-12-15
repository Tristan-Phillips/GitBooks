# Regular Expressions

### Wildcards

```
//Wildcards
c	Any character represents itself apart from those mentioned below. Thus c matches the character c.
?	Matches any single character. It is the same as . in full regexps.
*	Matches zero or more of any characters. It is the same as .* in full regexps.
[abc]	Matches one character given in the bracket.
[a-c]	Matches one character from the range given in the bracket.
[!abc]	Matches one character that is not given in the bracket. It is the same as [^abc] in full regexp.
[!a-c]	Matches one character that is not from the range given in the bracket. It is the same as [^a-c] in full regexp.
```

### Code Examples

```cpp
//Example of setting a lineEdit regex
m_lineEdit_regex->setValidator(new QRegularExpressionValidator(QRegularExpression("[A-Z]{3}[a-z]{2}[0-9]{5}[a-zA-Z0-9]{10}")));
```

```cpp
//Example of two different regex function implementations
bool Regex::isValid(QString text)
{
    // Create a regular expression for validating an email address
    QRegularExpression re("([a-zA-Z0-9\\.\\-]+)@([a-zA-Z0-9\\-]+)\\.([a-zA-Z0-9\\.]+)");
    //Required to test the regular expression
    QRegularExpressionMatch match = re.match(text);
    if (match.hasMatch()) {
        qDebug() << "Matched!";
        return true;
    } else {
        qDebug() << "Not matched!";
        return false;
    }
}

bool Regex::strangeRegex(QString text)
{
    QRegularExpression re("([a-zA-Z0-9\\.\\-]+)@([a-zA-Z0-9\\-]+)\\.([a-zA-Z0-9\\.]+)");
    //Include QT += GUI
    QRegularExpressionValidator validator(re);
    int pos = 0;

    if (validator.validate(text, pos) == QValidator::Acceptable) {
        qDebug() << "Matched!";
        return true;
    } else if(validator.validate(text, pos) == QValidator::Intermediate) {
        qDebug() << "Intermediate!";
        return false;
    } else if(validator.validate(text, pos) == QValidator::Invalid) {
        qDebug() << "Not matched!";
        return false;
    }
}
```
