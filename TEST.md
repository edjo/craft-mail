
# Checkout Plugin for Craft CMS 3.x #
  Plugin to make payments and manage integrated with API's Stripe and Paypal

## Requirements

 - Craft 3.0 (beta 28)+  
 - PHP 7.0+  
 - [PHP Intl extension](http://php.net/manual/en/book.intl.php) 

## Installation ##

 2. Install with Composer
	In the `composer.json` file:  
```  
{  
  ...  
  "minimum-stability": "dev",  
  "prefer-stable": true,  
  "repositories": [  
    {  
        "type": "vcs",  
        "url":  "git@bitbucket.org:okam/craft-checkout-plugin.git"  
    }  
  ],  
  "require": {  
    ...  
    "okam/checkout": "dev-master"  
  }  
  ...  
}  
```
 3. Install plugin in the Craft Control Panel under Settings > Plugins  
 4. Run the migrate command to install the plugin entities in the database:  
```  
./craft migrate/up --plugin=checkout  
```

### Installation notes ###

 - After some installation test, we noticed that the migrate did not work and the entities were not inserted in the database, but the plugin registers in the migrate table as if it happened well. So it is necessary to delete migrate records from the plugin in the migrations table and rerun the command to update.
 -  Because this is a private repository, the installation server must have ssh access to the repository.



## Example of usage ##
On the payment page where the form should appear, you must enter the following code:  
```  
{{  
    craft.checkout.createForm({  
        group: 2,  
        user: {  
            id: 1234,  
            email: 'edjobrandao@gmail.com'  
        },  
        currency: "CAD",  
        cityCart: {  
            taxes: [  
                {  
                    name: "Taxes of NYC (10%)",  
                    amount: "22.00"  
                },  
                {  
                    name: "Food taxes (5%)",  
                    amount: "03.00"  
                }  
            ],  
            items: [  
                {  
                    id: 103,  
                    quantity: 1,  
                    product: {  
                        id: 1005,  
                        name: "Member (bus)",  
                        price: "34.00"  
                    }  
                },  
                {  
                    id: 104,  
                    quantity: 1,  
                    product: {  
                        id: 1004,  
                        name: "Invite (bus)",  
                        price: "34.00"  
                    }  
                },  
                {  
                    id: 103,  
                    quantity: 1,  
                    product: {  
                        id: 1004,  
                        name: "Catering menu",  
                        price: "11.00"  
                    }  
                }  
            ]  
  
        },  
        debCart: {  
            taxes: [  
                {  
                    name: "Transaction fees",  
                    amount: "08.00"  
                }  
            ],  
            items: [  
                {  
                    id: 103,  
                    quantity: 1,  
                    product: {  
                        id: 1003,  
                        name: "Membership International",  
                        price: "08.00"  
                    }  
                }  
            ]  
  
        }  
    })  
}}  
```

## CP Settings ##
In the Control Panel you can set the settings for the operation of payments.  
**Live Mode** _Enabled makes PayPal and Stripe payments in live mode._  
**Stripe Credentials** _Fill out the Stripe credentials for Live and Test Mode and check out the webhook URL._  
**PayPal Credentials** _Fill out the PayPal credentials for Live and Sandbox Mode._  

## Features ##

 - [x] Generate Payment Stripe
 - [x] Stripe List Transactions
 - [x] Stripe view more payment details
 - [x] Generate Payment PayPal
 - [x] PayPal List Transactions
 - [ ] PayPal view more payment details
 - [ ] PayPal IPN notification (Update payment status)
 - [ ] Email after payment approved
