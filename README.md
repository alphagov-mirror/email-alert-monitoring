# Email alert monitor

GOV.UK provides email alerts. This repo provides scripts that verify that
emails have been sent for certain publications.

Currently the script looks at [drug and medical advice
alerts](https://www.gov.uk/drug-device-alerts) and [foreign travel advice
alerts](https://www.gov.uk/foreign-travel-advice).

### Drug and medical advice alerts

An email address has been subscribed to these alerts (via [the email signup page](https://www.gov.uk/drug-device-alerts/email-signup)).

Every hour, we look at [the public RSS feed for alerts](https://www.gov.uk/drug-device-alerts.atom). We then check the
email address has received an email for these publications via the
[Google Gmail API](https://developers.google.com/gmail/api/).

The `EMAILS_THAT_SHOULD_RECEIVE_DRUG_ALERTS` environment variable
contains the email address that has been subscribed to receive these
emails.

### Travel advice alerts

An email address has been subscribed to these alerts (via [the email signup page](https://www.gov.uk/foreign-travel-advice/email-signup)).

Every hour, we look at [the content store feed for alerts](https://www.gov.uk/api/content/foreign-travel-advice). We then
check the email address has received an email for these publications via
the [Google Gmail API](https://developers.google.com/gmail/api/).

The `EMAILS_THAT_SHOULD_RECEIVE_TRAVEL_ADVICE_ALERTS` environment
variable contains the email address that has been subscribed to receive
these emails.

## Technical documentation

### Running

`bundle exec rake run` for the drug and medical device alert checker

`bundle exec rake run_travel_alerts` for the travel advice alert checker

Both rake tasks will exit normally and not output anything if everything
is OK.

If they find that some alerts have not been sent out, they will print the
missing alerts and exit with a non-zero exit code. When reported to Icinga
by Jenkins, this will alert developers.

### Running the test suite

`bundle exec rspec`

## Licence

[MIT License](LICENCE.txt)
