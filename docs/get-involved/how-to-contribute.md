# How to contribute

This is a living documentation site, meaning we need the community's help to maintain and update the content. Any contribution, from writing whole sections and translations to correcting spelling and grammar mistakes will be greatly appreciated.

<https://twitter.com/EridianAlpha/status/1651666798847094792>

Use this GitBook invite link to suggest edits and new content directly on GitBook:

<https://app.gitbook.com/invite/5TLAFycQGS1YA3kIVVOf/mApYtvFWf7QnDjZJdUhf>

You can earn GitPOAPs by contributing directly to the EthStaker Knowledge Base (a [contributor↗](https://www.gitpoap.io/gp/881)) and by asking a question that leads to content being created (a [supporter↗](https://www.gitpoap.io/gp/923)).

[![EthStaker Knowledge Base Contributor GitPOAP 2023](https://www.gitpoap.io/_next/image?url=https%3A%2F%2Fassets.poap.xyz%2Fgitpoap3a-2023-ethstaker-knowledge-base-contributor-2022-logo-1671596764627.png&w=750&q=75)](https://www.gitpoap.io/gp/881)[![EthStaker Knowledge Base Supporter GitPOAP 2023](https://www.gitpoap.io/_next/image?url=https%3A%2F%2Fassets.poap.xyz%2F2023-ethstaker-knowledge-base-supporter-2022-logo-1672411990803.png&w=750&q=75)](https://www.gitpoap.io/gp/923)

To suggest changes or add new content please visit our [EthStaker Github↗](https://github.com/ethstaker/ethstaker-knowledgebase) or if you have any questions please join our [Discord↗](https://www.google.com/url?sa=t\&rct=j\&q=\&esrc=s\&source=web\&cd=\&cad=rja\&uact=8\&ved=2ahUKEwjpm6nC5K78AhUBi1wKHaxHCF8QFnoECAsQAQ\&url=https%3A%2F%2Fdiscord.com%2Finvite%2FucsTcA2wTq\&usg=AOvVaw0U61EK\_8NaT71SEZlw3aJS).&#x20;

Please create a pull request for any changes you want to make and we'll review it as soon as possible.

* [Documentation standardization notes](#documentation-standardization-notes)
* [Creating/Updating tables of contents](#creatingupdating-tables-of-contents)
* [Glossary and FAQ heading ordering](#glossary-and-faq-heading-ordering)

## Documentation standardization notes

Please use these notes when writing for this knowledge base to maintain a standardized format.

* Use [relative links ↗](https://github.blog/2013-01-31-relative-links-in-markup-files/) to navigate between different files within this knowledge base.
  * `[Other file link](/other_file)` → [Privacy Policy](../../privacy-policy)
* Use anchor links to headings within the same file.
  * `[Anchor link](#heading-anchor)` → [Anchor link](#documentation-standardization-notes)
* Combine relative links to other files with anchor links.
  * `[Other file anchor link](other_file#heading-anchor)` → [Other file link](#documentation-standardization-notes)
* Show when a link is referencing an external site by adding the ↗ icon at the end of the link.
  * `[External site link ↗](https://example.com)` → [External site link ↗](https://example.com)
* Create an image that's also a link.
  * `[![image-text](https://some.site/your-image.jpg)](https://some.site/your-link.html)`

## Creating/Updating tables of contents

The tables of contents are created using a VSCode extension [Markdown All in One ↗](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) using the command `Create Table of Contents` (in the [VS Code Command Palette ↗](https://code.visualstudio.com/docs/getstarted/userinterface#\_command-palette)) to insert a new table of contents. It should then automatically be updated when a file is saved.

Add the tag `<!-- omit in toc -->` to any headings you do not want to be included in the Table of Contents.

```
# HEADING <!-- omit in toc -->
```

## Glossary and FAQ heading ordering

When adding items to the Glossary and FAQ it's important that they remain in alphabetical order so it's easier to navigate. As there is no native way to achieve this in Markdown, you can use this bash script to reorder the headings.

> The file name `alphabetical-ordering.sh` has been added to the .gitignore file.

```
touch alphabetical-ordering.sh
chmod 700 alphabetical-ordering.sh
```

Edit the new file with your preferred text editor.

```
#!/bin/bash
# Reorder glossary and store just the reordered content in a temp file
perl -0777 -ne '
    (undef,@paragraphs) = split /^##(?=[^##])/m;
    print map {"##$_"} sort @paragraphs;
' staking-glossary.md > staking-glossary-temp-1.md

# Delete everything after the first --- in and store in a temp file
sed '/---/q' staking-glossary.md > staking-glossary-temp-2.md

# Combine the two files
cat staking-glossary-temp-2.md > staking-glossary.md
cat staking-glossary-temp-1.md >> staking-glossary.md

# Delete the temp files
rm staking-glossary-temp-1.md
rm staking-glossary-temp-2.md


# Reorder FAQ and store just the reordered content in a temp file
perl -0777 -ne '
    (undef,@paragraphs) = split /^##(?=[^##])/m;
    print map {"##$_"} sort @paragraphs;
' faq.md > faq-temp-1.md

# Delete everything after the first --- and store in a temp file
sed '/---/q' faq.md > faq-temp-2.md

# Combine the two files
cat faq-temp-2.md > faq.md
cat faq-temp-1.md >> faq.md

# Delete the temp files
rm faq-temp-1.md
rm faq-temp-2.md
```

Run the script.

```
./alphabetical-ordering.sh
```

> This was a quick script, so if you have any improvements please update it here!
