============
Glossary
============

Current Configuration
======================
The current configuration uses:

* the Glossary taxonomy, configured as a "translate" multilingual taxonomy (so that each language has its own terms)
* the lexicon module, which adds a filter to WYSIWYG content to automatically highlight glossary terms by:
  
  * matching on the exact word (so that the glossary term eviction will be associated with eviction but not evict or evicting).
  * is case insensitive
  * only picks up the first instance in the entity (this has been problematic with paragraphs as it picks up the first instance in each paragraphs bundle rather than just the first entity in the node)
  * is supposed to ignore terms in headers but this does not work
  * ignores text wrapped in the no-lexicon tags
  * links to the term in a glossary page
  * breaks the glossary across multiple pages by letter
  * links related terms
  

.. note::
   Lexicon has not been ported to Drupal 8
   
   
   