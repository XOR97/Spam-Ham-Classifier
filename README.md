# Spam-Classifier

A general purpose spam classifier implemented using the naive Bayes probability approach.
This was created as a proof of concept spam filter for my undergrad college course.

The classifier first takes a body of known spam and ham (non-spam) emails to
evaluate. Then, it evaluates each email in a test body of emails as spam or ham,
with the difference between ham and spam only known to the classifier for the
purpose of calculating the success rate.

Several parameters can be changed to optimize the effectiveness of the
classifier. By tweaking these parameters, rates in the upper 90% range for both
spam and ham classification can be reached.

A sample of Apache SpamAssassin’s public corpus of spam and ham
emails was used for testing.

## Demo Usage

Run the script in terminal via

    python spam_classifier.py spam_examples ham_examples spam_test ham_test
           -init_prob_spam 0.7 -occurence_threshold 5 -phrase_length 5

       positional arguments:
         spam_examples         spam example messages folder
         ham_examples          ham example messages folder
         spam_test             test messages folder
         ham_test              test messages folder

       optional arguments:
         -h, --help            show this help message and exit
         -init_prob_spam INIT_PROB_SPAM
                               initial probability of a message being spam (0-1)
         -occurence_threshold OCCURENCE_THRESHOLD
                               number of times a word must appear in spam and ham
                               messages overall
         -score_threshold SCORE_THRESHOLD
                               spam score above which a message must be rated to be
                               considered spam (0-1)
         -phrase_length PHRASE_LENGTH
                               maximum length of word phrases considered (higher
                               phrase lengths will impact performance)


After evaluating the contents of the emails (which can take a few seconds given
that a phrase length of 5 was used), the classification success rates are
displayed:

    Spam success rate: 98.00%
    Ham success rate: 99.50%

## Few things to consider...

Despite the clear benefits of filtering spam using naive bayesian probabilities, there are still disadvantages.
One attack that filters using naive bayes probability might be susceptible to is a method called bayesian poisoning.
This method involves spammers injecting non­spammy words into their spam messages in order to trick the filter into classifying them as ham.

Another method that spammers use to circumvent spam detection is by putting the text of their email into an image,
which bayesian spam filters typically ignore. This can be combated by using optical character recognition in order to extract text from images.
