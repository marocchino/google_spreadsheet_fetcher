# GoogleSpreadsheetFetcher

Use OAuth 2 authentication to retrieve data from Google Spreadsheet.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'google_spreadsheet_fetcher'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install google_spreadsheet_fetcher

## Usage

- Make project. https://cloud.google.com/resource-manager/docs/creating-managing-projects
- Enable Google Drive API
- Make OAuth 2.0 Client. (other)
- Download client secret json


```ruby
sheet_key = 'example_sheet_id'

GoogleSpreadsheetBulkFetcher.configure do |config|
  config.client_secrets_file = 'client_secrets_file_path.json'
  config.credential_store_file = 'credential_store_file_path.json'
end

user_id = 'sample'

fetcher = GoogleSpreadsheetFetcher::Fetcher.new(credential_store_file, user_id, sheet_key)

fetcher.fetch_all_rows_by!(index: 0)
fetcher.fetch_all_rows_by!(title: 'sheet_title')
fetcher.fetch_all_rows_by!(sheet_id: 1234567890)


# or, you can do a bulk fetching. In this case, you only need to access the API once,
# but it will take a little longer on first fetch.
fetcher = GoogleSpreadsheetFetcher::BulkFetcher.new(sheet_key, user_id)
fetcher.fetch

fetcher.all_rows_by!(index: 0)
fetcher.all_rows_by!(title: 'sheet_title')
fetcher.all_rows_by!(sheet_id: 1234567890)
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/taka0125/google_spreadsheet_fetcher.

