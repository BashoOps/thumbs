# Thumbs

A simplified integration robot.

![Logo][logo]
[logo]: https://ryanbrownhill.github.io/github-collab-pres/img/thumbsup.png

### What does it do ?

It merges a pull request for you after doing validation.
 
 * (merge,build,test success and >=2 reviewers)

### How does it work ?

* When a comment is made on a pull request, a github webhook is called on /webhook
* Using the webhook payload, it looks up the pull request.
* It verifies if the pr is valid for merge:
  * Merges locally 'git merge feature_branch'
  * Builds 'make build'
  * Test 'make test'
  * Ensures PR contains a minimum of 2 non author review comments
* Adds a comment on the PR with the build status
* After final validations, request a PR merge through github API 


## Installation

```
> git clone https://github.com/davidx/thumbs.git
> cd thumbs
> rake install
```
## Setup
### test
For testing 
```
export GITHUB_USER=ted
export GITHUB_PASS=pear

export GITHUB_USER=ted
export GITHUB_PASS=pear

export GITHUB_USER1=bob
export GITHUB_PASS1=apple
```
### production
For normal operation, only a single set of github credentials is needed.
```
export GITHUB_USER=ted
export GITHUB_PASS=pear
```

### test webhooks 
##### In a separate window, start ngrok to collect the forwarding url
```
> ngrok -p 4567
```
##### This will display the url to use, for example:
```
Forwarding                    http://699f13d5.ngrok.io -> localhost:4567        
```

##### Go to the Github repo Settings->Webhooks & services" and click [Add webhook].
    Set the Payload URL to the one you just saved. add /webhook path. 

    Example: http://699f13d5.ngrok.io/webhook

    Checkbox: Send me Everything

## Test
```
> rake test
```
## Usage

```
> rake start
# Now go to your favorite pull request on github, leave a comment and watch the magic happen.
```

### Example: https://github.com/BashoOps/prtester/pull/189


