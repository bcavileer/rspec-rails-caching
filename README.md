# RSpec Rails Caching

Provides a cache store for recording and matchers for testing cache events in
Rails controller tests.

## Installation

Add this line to your application's Gemfile:

    gem 'rspec-rails-caching'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rspec-rails-caching

## Usage

Set `config.action_controller.perform_caching = true` in `config/environments/test.rb`

This gem captures the actual cache events for each request. In a controller
example group, use a proc or a lambda around the action for matching:

    describe WidgetsController, type: :controller do
      it "should cache the show action" do
        ->{ get :show, id: 123 }.should cache_page('/widgets/123')
      end

      it "should expire the update action" do
        ->{ put :update, id: 123 }.should expire_page('/widgets/123')
      end
    end

### Available matchers:

* `cache_page` / `expire_page`
* `cache_fragment` / `expire_fragment`
* `cache_action` / `expire_action`

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
