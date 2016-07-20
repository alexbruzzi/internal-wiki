# Creating Hooks in Octo

Hooks are primarily defined in `Octo::OctoHooks`.

Existing hooks list are:

- after\_app\_init
- after\_app\_login
- after\_app\_logout
- after\_page\_view
- after\_productpage\_view

Two scenarios are possible

- Add more callbacks to one of these hooks
- Create new hooks

### Adding more callbacks

- Define your custom tasks in the module override, like

```
lang=ruby
module Octo

  module OctoHooks

    # Define the custom tasks that need to be done
    #   upon various hooks
    Octo::Callbacks.after_productpage_view lambda { |opts|
      update_recommenders opts
    }

    # Extend the methods here
    module ClassMethods

      # Updates the recommenders
      # @param [Hash] opts The options hash as passed
      def update_recommenders(opts)
        user = opts[:user]
        product = opts[:product]

        if user and product
          recommender = Octo::Recommender.new
          recommender.register_user_product_view(user, product)
          recommender.register_user_action_time(user, Time.now.floor)
        end
      end

    end
  end
end
```

#### Adding new hooks

- Similar like above


