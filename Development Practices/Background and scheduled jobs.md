Our goal is to have applications that process incoming web requests in a timely fashion.
Some requests don't just manipulate data from your database, but can:

- send emails
- send push notifications
- execute transactions
- generate PDFs
- interact with 3rd party APIs
- do other long-running requests, eg. updating database indices (Algolia)

In this case, the web request can take up much more of your resources, which will impact the speed of page response times and potentially result in page timeouts during high traffic.

## Background jobs
The solution to these problems is to extract the part that does the heavy-lifting and execute it asynchronously.

The extracted part is called a *background job* which can be scheduled or executed at the time of the incoming request in another process.

To get background jobs to work, we need the following infrastructure:

- database to store jobs - [redis](https://github.com/redis/redis-rb)
- processor that executes jobs - [sidekiq](https://github.com/mperham/sidekiq)

Configuring Sidekiq to work with Redis can be found [here](https://github.com/mperham/sidekiq/wiki/Using-Redis).
After you [setup](https://github.com/mperham/sidekiq/wiki/Getting-Started) a worker (background job) you can hook it up wherever is required and choose when it's going to be executed.

### Error handling
Another great benefit for using background jobs is improving fault tolerance, especially if you have an API that communicates with another.

We can never be 100% sure that the dependent API works OK, which could cause errors in the database or 500 HTTP errors.

Sidekiq background jobs provide [options](https://github.com/mperham/sidekiq/wiki/Advanced-Options#workers) that are defined as class methods which can be used to improve error handling.

### Best practices
Some of the best practices have been covered in the official [Sidekiq Wiki pages](https://github.com/mperham/sidekiq/wiki/Best-Practices).

### Active Job
Active Job is a framework for declaring jobs and making them run on a variety of [queuing backends](https://guides.rubyonrails.org/active_job_basics.html#starting-the-backend).

To setup Sidekiq as a queuing library for Active Job read [this Wiki](https://github.com/mperham/sidekiq/wiki/Active-Job).

## Scheduled jobs
Sometimes a service needs to be run recurrently and not in a HTTP request lifecycle:

- every N (seconds/minutes/hours/days)
- on a certain day of every month
- on a certain hour of every day
- etc...

This is where [sidekiq-scheduler](https://github.com/moove-it/sidekiq-scheduler) comes in handy.
It also provides the `cron` option for specifying when the service will be called if you prefer or require it.

## Sidekiq Monitoring
API's usually require a dashboard interface for the admin users. It makes sense to also include a monitoring tool that has a lot of useful info in regards to background jobs.

You can use [built-in methods](https://github.com/mperham/sidekiq/wiki/Monitoring#devise) in your `config/routes.rb` file to enable this feature.
#### _NOTE:_
If you have nginx configured to only lookup assets in the `current/public` folder, the Monitoring dashboard will load without the `sidekiq/web` assets. To solve this, you have to create a symlink to the Sidekiq assets folder using the `link_sidekiq_assets` mina task:

```ruby
task :deploy do
  invoke :'git:ensure_pushed'
  deploy do
    invoke :'git:clone'
    invoke :'deploy:link_shared_paths'
    invoke :'bundle:install'
    invoke :'secrets:pull'
    invoke :'rails:db_migrate'
    invoke :'rails:assets_precompile'
    invoke :'deploy:cleanup'

    on :launch do
      invoke :link_sidekiq_assets
      invoke :restart_application
      invoke :restart_sidekiq
    end
  end
end
```

In case your Sidekiq monitoring tool is namespaced behind an authenticated route:

```ruby
authenticate :administrator do
  mount Sidekiq::Web => '/admin/sidekiq'
end
```

then you also need to:

`set :sidekiq_web_namespace, :admin`

in your `config/deploy.rb` file.


### Interesting articles:
* [Which Ruby background job framework is right for you?](https://scoutapm.com/blog/which-ruby-background-job-framework-is-right-for-you)
* [Improving Rails Performance with Better Background Jobs](https://rollout.io/blog/improving-rails-performance-better-background-jobs/)
* [How to use sidekiq with devise to send emails without devise-async](https://stackoverflow.com/a/56265427/1339894)
