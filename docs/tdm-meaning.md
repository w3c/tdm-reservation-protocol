# TDM: what does it mean in practice? 

It is difficult to give strict boundaries to the notion of Text and Data Mining. The EU Copyright Directive offers the following definition:

*(2) ‘text and data mining’ means any automated analytical technique aimed at analysing text and data in digital form in order to generate information which includes but is not limited to patterns, trends and correlations”*

Further details are provided in Recital 8:

*“New technologies enable the automated computational analysis of information in digital form, such as text, sounds, images or data, generally known as text and data mining. Text and data mining makes the processing of large amounts of information with a view to gaining new knowledge and discovering new trends possible.”*

In a white paper, the EPC introduces it as  	

*“The ability of new technology to extract meaningful information from vast amounts of data.”*

## TDM vs AI/ML

Text and data mining techniques are important tools for preparing and analyzing data for use in most AI/ML (*) applications. It is particularly the case for any solution involving large training sets, especially generative AI solutions like GPT-4 or Midjourney. 

In March 2023, Thierry Breton, Commissioner for Internal Market of the European Union, gave [useful precisions about the applicability of the TDM exceptions defined in DSM Directive for AI solutions](https://www.europarl.europa.eu/doceo/document/E-9-2023-000479-ASW_EN.html). This answer enforces that for the EU Commission, the use of web content by AI solutions falls into the scope of the Articles 3 and 4 of the DSM Directive. 

## TDM vs search engines

To our knowledge, search engines don't apply TDM techniques to the content they crawl and index; therefore, web crawlers are not affected by the TDM reservation techniques defined by this group. 

To be certain that TDM opt-out does not impact the indexation of web content by search engines, we didn't even try to extend robots.txt for the sake of defining the TDM reservtion protocol. The techniques used in the TDMRep specification are similar to those used in robots.txt because the latter are globally considered simple, flexible and powerful, but they do not overlap. For more information about robots.txt, you can read [robots for non techies](./robots.html). 

* AI/ML stands for Artificial Intelligence / Machine Learning

