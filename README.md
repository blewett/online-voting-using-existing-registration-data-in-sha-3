# Online Voting System Discussion

The “mail in voting” of the 2020 election produced a record turnout.  In many states ballots were sent out to all registered voters.  Signatures were required on most of the mail in ballots.  To register to vote one provides five pieces of data:  name, address, date of birth, social security number, and signature samples.  We always want to preserve the traditional voting systems of registration and voting / polling.  At the polling locations, a signature is required to be compared with the signature provided at registration and/or the last vote.  This is done by the people running the polling location.

There were news reports of irregularities in the processing of the signatures of the mail in ballots in the 2020 election.  Some reports state that signature verification was disabled or the verification was done in high percentages through human intervention – the term is adjudicated.  Adjudication is fairly common for many other reasons with paper ballots.  My signature varies greatly day to day.  Algorithms for comparing signatures are heuristics at best.  At polling places signatures are all adjudicated – that is examined by poll workers.

Online voting uses the tools of the Internet to allow voting from homes, residences, and anywhere one might want to cast a vote.  The HTTPS protocol in wide use on the Internet guards against “man in the middle” attacks.  Online voting can be easily implemented with what has been traditionally collected for voter registration and it will be more secure than the mail in voting systems that were used in 2020.  Signature verification is replaced by comparison of data already collected which can be exactly or precisely matched.  Date of birth and the last four digits of one’s social security number are good examples.  Where available, one could also add a code sent to the voter’s cellphone as is done by Amazon and financial institutions.  Online voting and electronic storage of votes would increase turnout and provide a much quicker and trusted vote count/tabulation.  A quick and transparent tabulation is important for restoring confidence in the voting system.

The chaos of the Gore v. Bush election was related to the problems one finds in counting ballots cast on physical media; usually some paper product.  Debate over physical ballot media also occurred in the 2020 election.  The notion with online voting is that completed ballots would be sent by the voter directly to the government hosted ballot database, all with no human intervention, no rejected or crumpled ballots, no ballots lost in the mail, and no hanging chad as occurred in Gone v. Busch.  On a small computer one can easily count a million votes per second in a computer based ballot database – all without any human intervention.  The vote counting software can also be published for complete transparency.  It is very simple code, just a few lines that can be quickly reviewed by even novices.  One can also allow voters to review / verify votes previously cast – we discuss that later.

Consider this implementation of online voting.  Ballots would be sent out as in 2020.  The ballots would include a unique, human readable, “ballot number”.  This ballot number would be the only change to the ballot that was sent to all voters.  Numbering the ballots means that only legal ballots can be cast.  That number would be included by the voter when casting the vote online.  The systems would allow for only one vote per numbered ballot.  The ballot numbers are never associated with the identity of the voter – thus keeping the identity of the voter secret.  Some of the mail in ballots used in the 2020 election did include identification codes, but there were reports of those codes were not used.  The 2020 codes were not intended for human readability and use.

This repository contains doc and ppt files describing a reliable online voting system based on existing voter registration data and common Internet, and data processing techniques.
