# Online Voting System Discussion

![alt text](https://github.com/blewett/online-voting-using-existing-registration-data-in-sha-3/blob/main/images/vote_form.jpg?raw=true)

This is a prototype implementation of an online voting system.  This discussion was started prior to the 2020 election and now seems more relevant.  The prototype implementation uses data already collected in the voter registration process and uses that to provide multi-factor verification.  Voting and the counting of votes should all be processed via automation.  There is no need for human intervention once the vote is cast.  All cryptographic work is done by code running on the server.  In the case of this prototype that code is all written in php.  The primary cryptographic tool is sha-3 hashing - again all performed in php.  The code is designed to be easily setup on most modern computing equipment under Linux, Apple macos, and Windows 10.  There is no compilation required.  Download the code and read the document.

![alt text](https://github.com/blewett/online-voting-using-existing-registration-data-in-sha-3/blob/main/images/vote_login.jpg?raw=true)

We run a local user level php server for debugging and testing.  The php server is invoked with the following:

php -S 127.0.0.1:8181

That sets up a web server on port 8181 - http://localhost:8181.

The “mail in voting” of the 2020 election produced a record turnout.  In many states ballots were sent out to all registered voters.  Mail in ballots have become one of the new voting standards.  Signatures were required on most of the mail in ballots.  To register to vote one provides five pieces of data:  name, address, date of birth, social security number, and signature samples.  I always want to preserve the traditional voting systems of registration and voting / polling.  If someone wants to vote at a polling location rather than by some other means, I think the polling option should always be available.  At the polling locations, a signature is required to be compared with the signature provided at registration and/or the last vote.  This comparison is done by the people running the polling location.

https://www.vote.org/voter-id-laws/
https://ballotpedia.org/Voter_identification_laws_by_state

There were news reports of irregularities in the processing of the signatures of the mail in ballots in the 2020 election.  Some reports state that signature verification was disabled or the verification was done in high percentages through human intervention – the term is adjudicated.  Adjudication is fairly common for many other reasons with paper ballots.  My signature varies greatly day to day.  Algorithms for comparing signatures are heuristics at best.  Again, at polling places signatures are all adjudicated – that is examined by poll workers.

Online voting uses the tools of the Internet to allow voting from homes, residences, and anywhere one might want to cast a vote.  The HTTPS protocol is in wide use on the Internet and guards against “man in the middle” attacks.  Online voting can be easily implemented with what has been traditionally collected for voter registration and it will be more secure than the mail in voting systems that were used in 2020.  I want to emphasize that point.  Signature verification is replaced by comparison of data already collected which can be exactly or precisely matched.  Date of birth and the last four digits of one’s social security number are good examples.  Where available, one could also add a code sent to the voter’s cellphone as is done by Amazon and financial institutions.  Online voting and electronic storage of votes would increase turnout and provide a much quicker and trusted vote count/tabulation.  A quick and transparent tabulation is important for restoring confidence in the voting system.

The chaos of the Gore v. Bush election was related to the problems one finds in counting ballots cast on physical media; usually some paper product.  Debate over physical ballot media also occurred in the 2020 election.  The notion with online voting is that completed ballots would be sent by the voter directly to the government hosted ballot database, all with no human intervention, no rejected or crumpled ballots, no ballots lost in the mail, and no hanging chad as occurred in Gore v. Bush.  On a small computer one can easily count a million votes per second in a computer based ballot database – all without any human intervention.  The vote counting software can also be published for complete transparency.  It is very simple code, just a few lines that can be quickly reviewed by even novices.  With online voting, one can also allow voters to review/verify votes previously cast – we discuss that later.

Consider this implementation of online voting.  Ballots would be sent out as in 2020.  The ballots would include a unique, human readable, “ballot number”.  This ballot number would be the only change to the ballot that was sent to all voters.  Numbering the ballots means that only legal ballots can be cast.  That ballot number would be included by the voter when casting the vote online.  The systems would allow for only one vote per numbered ballot.  The ballot numbers are never associated with the identity of the voter – thus keeping the identity of the voter secret.  This uses the same technology as that used in online banking or shopping – that is enter and verify. 

Some of the mail in ballots used in the 2020 election did include identification codes, but there were reports of those codes were not used.  The 2020 codes were not intended for human readability and use.  The ballot numbers would be assigned by each voting area and held in a voting verification database.  The database would include a one way encryption (i.e. hash code) of the ballot number, a one way registration hash representing the voter, a time stamp, and a flag if the ballot has been used.  The ballot number could also be emailed or texted to the voter as we want the voting process to be as green as possible – no paper.  The local voter registrar is the only entity in the voting process that would have the voter identification.  In the verification database the identification is done via the encryption hash.  The ballot number is also never visible in the system as it is stored as a one way hash.

The ballot number acts as an additional factor to verify the voter to the system.  The ballot number guarantees that the voter is using a legal ballot.  The system also enforces that the ballot can only be used by the assigned voter.  This is more secure than the long trusted absentee balloting system we have used for decades.  And those ballots are handled by many people on the way to being counted.  Adding the ballot number is the equivalent of two factor verification that is, again, used with Amazon purchases or is commonly used in financial transactions.

Online voting is a two step process: voter login and ballot casting.  Voters login to the voting system using their name, address, and date of birth and possibly the last four digits of your social security number.  We would like to see voters get a registration number which could be used in lieu of a signature.  Voters are limited to one login per vote – that is only one vote per voter.  The login would give access to the ballot casting screen.  After login the ballot screen would be displayed – possibly from another web server.

On the ballot screen the voter would enter the “ballot number”.  The voter identification and the ballot number are never included together.  A doubly encrypted voter, one way, hash is sent out with the ballot screen and the ballot number is entered into that screen by the voter.  The voter hash maintained by the system is never visible outside of the database.  Again, the database version of the voter identity hash is encrypted prior to it being sent out with the ballot webpage.  Ballot numbers are checked to avoid multiple votes on a single ballot.  Ballot numbers can only be used once.  Voters can only vote once.

The numbers produced by the encryption hash are computationally very difficult (impossible given computer time) to link back to the identity of the voter.  Think of adding all of the digits in your name, address, date of birth, and last digits of your social security number and then multiplying it by a hidden key.  The hash is calculated again in real time by the login software and used by the election board when sending out the ballot collection screen to the voter.  Again, the key to that encryption would change over time to keep the voter’s registration hash from being reused.  All of this is standard cryptographic processing and not seen by the voter.

Completed ballots would be sent directly to the government polling website.  Ballots would be entered into a cast ballot database.  The cast ballots would include an encrypted ballot number.  All of the processing of the cast ballots would be automated without human intervention thus avoiding the problems with physical voting media.  As mentioned above, the HTTPS Internet protocol protects against “man in the middle” attacks.  That is HTTPS is a secure transport that guarantees secure communication with web servers.  There are also secure techniques for hiding one's IP address (e.g. Tor).  There is not a pressing need to hide the IP address.  People can be observed entering polling places.

The ballot number that is sent to the voter could be an encrypted number.  Encryption using the advanced encryption standard (AES) or other standard would produce a small number that could be easily entered by the voter.  The voter need not go through any tedious encryption processing.  The voter only sees the ballot number and that number is opaque to the voter – that is has no meaning other than being a number.

Information processing has made great strides.  As votes pour in they would be “journal-ed” to avoid loss and to enable processing that we often refer to as a “chain of custody” verification.  Journaling also allows for accurate vote count monitoring by region.  Again, this would be all automated without any human intervention.  The code for an online voting system should all be made public.  There is no reason to keep the code hidden/secret.

After casting ballots, voters would like to be able to review the cast ballots as a way to personally verify that their ballot was recorded correctly.  When a legal ballot is cast online, the system would return a “cast number” that can be used to later inspect the cast ballot.  To review a cast ballot, the voter would use the ballot number and the cast number to view the cast vote.  The cast ballot database would store the encrypted versions of the ballot number and the cast number.  Those two numbers could be used at a later date to retrieve and examine the cast ballot.  The voter’s identity would not be revealed using this method.  Legal access to the voting system would be preserved.

One has to compare online voting with mail in voting as the test for viability.  There is a “consensus” argument that online voting will never be as secure as paper media based voting.  The scientific rationale for that argument is usually completely missing.  Every time voting media is physically handled there is the possibility for error or worse yet fraud.  From Ballotpedia, a non partisan organization, rejected ballot percentages are around one percent of the mail in/absentee ballots.  The numbers for the 2020 election are still out in many locales.  Consider the many human steps involved in mailing back a ballot and that ballot being tabulated by running the ballots through tabulating machines.  We need to move to online voting.  It is time.

https://ballotpedia.org/Election_results,_2020:_Analysis_of_rejected_ballots

This repository contains doc and ppt files describing a reliable online voting system based on existing voter registration data and common Internet, and data processing techniques.  There doc file and a README-vote.txt file that explain how to setup and use the system across platforms.

Doug Blewett

doug.blewett@gmail.com
