+++
title = "Google Summer of Code 2019: Improve Article Recommendation Pipeline"
date = 2019-08-19T11:44:53+05:30
draft = false
tags = ["gsoc2019", "opensource"]
categories = ["Google Summer of Code 2019"]
+++

**GSoC Project Proposal:** [Improve Article Recommendation Pipeline](https://phabricator.wikimedia.org/T218971)

**Mentor:** [Bahodir Mansurov](https://phabricator.wikimedia.org/p/bmansurov/)

### Synopsis

The project improved the article recommendation pipeline by solving the various issues in the article-recommender projects.
The issues that were solved a part of the project are:

- [Remove duplicate Wikidata items from article recommendations](https://phabricator.wikimedia.org/T216721)
- [Recommendation API translation endpoint stopped working](https://phabricator.wikimedia.org/T215222)
- [Article recommendation API: replace WDQS with MW API](https://phabricator.wikimedia.org/T216750)
- [*morelike* recommendation API: Bulk import data to MySQL in chunks](https://phabricator.wikimedia.org/T211980)

### Links to code changes

**Merged:**

- [Remove duplicate Wikidata items from article recommendations.](https://gerrit.wikimedia.org/r/#/c/mediawiki/services/recommendation-api/+/512913/)
- [Throw appropriate error when wmAPI returns internal server error.](https://gerrit.wikimedia.org/r/#/c/mediawiki/services/recommendation-api/+/516732/)
- [Splits the request to MediaWiki API and Wikidata query service in batches.](https://gerrit.wikimedia.org/r/#/c/mediawiki/services/recommendation-api/+/517078/)

**Reviewed and waiting to get merged:**

- [Replace Wikidata Query Service with MediaWiki API](https://gerrit.wikimedia.org/r/#/c/mediawiki/services/recommendation-api/+/523779/)

**Work In Progress:**

- [Bulk import data to MySQL in chunks](https://gerrit.wikimedia.org/r/#/c/research/article-recommender/deploy/+/527571/)

### Outcome

Each task in the project had a noticeable outcome.

The first task made sure that the data returned by the `morelike endpoint` did not have duplicate data.
This ensured that the data we got from a single call to the API contained more wikidata items than what was being returned previously.

The second task made sure that the `translation endpoint` does not fail intermittently without returning a proper error code.
This helps us with debugging when some error arises. It also made sure that the API does not fail due to an error with the Wikidata Query Service.

The third task once merged will replace the internal call being currently made to Wikidata Query Service(WDQS) with a call to the MediaWiki API(MWAPI) when
the `translation endpoint` is called. This will decrease the number of requests being made internally thereby decreasing the time required by the
`translation endpoint`. It also decreases the time required by replacing the slower WDQS with a faster MWAPI.

The fourth task once completed makes sure that the script used to import the data generated by Hadoop into the database does not block the CPU.
It improves the CPU efficiency of the shared machines and allows to run other CPU tasks as well without them getting blocked.

### Acknowledgement

I would like to thank my mentor, [Bahodir Mansurov](https://phabricator.wikimedia.org/p/bmansurov/) for helping me throughout the program,
encouraging me with great feedback and guiding me towards project completion.