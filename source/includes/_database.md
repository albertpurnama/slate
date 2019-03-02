# Database

We use MySQL as our database server which is served locally in the digital ocean server. There are 3 main relations that we are going to look at.

1. BCC - Basic Client Characteristics
2. Errors
3. Performance

The rest of this section will describe each schema details. There will be [User Management](#user-management) relation which is a separate database from main analytics database.

## BCC Schema - Basic Client Characteristics

BCC relation is used to keep track of the types of visitors that visit the sample site. BCC does not include the visitors that visit the endgame analytics site.

Fields | Type | Null | Key | Default | Extra
------ | ---- | ---- | --- | ------- | -----
id | int(11) | NO | PRIMARY | NULL | auto_increment
session_id | varchar(100) | YES |  | NULL |  
timestamp | varchar(40) | YES |  | NULL |
device_type | varchar(40) | YES |  | NULL |
browser_type | varchar(255) | YES |  | NULL |
screen_height | int(11) | YES |  | NULL |
screen_width | int(11) | YES |  | NULL |
geo_location | varchar(255) | YES |  | NULL |

<aside class="notice">
The field <code>geo_location</code> may be removed in the future.
</aside>

## Errors Schema 

Errors relation is used to keep track of ANY errors that is happening in the example site. The logs are parsed in the NodeJS server, then it is logged in this relation.

Fields | Type | Null | Key | Default | Extra
------ | ---- | ---- | --- | ------- | -----
id | int(11) | NO | PRIMARY | NULL | auto_increment
session_id | varchar(100) | YES |  | NULL |  
timestamp | varchar(40) | YES |  | NULL |
code | int(11) | YES |  | NULL |
severity | varchar(10) | YES |  | NULL |
msg | varchar(255) | YES |  | NULL |


## Performance Schema

Performance relation keeps track of various performance indicators. Such indicators may include but not limited to `domInteractive`, `domLoading`, `domComplete`, `redirectCount`.

Fields | Type | Null | Key | Default | Extra
------ | ---- | ---- | --- | ------- | -----
id | int(11) | NO | PRIMARY | NULL | auto_increment
session_id | varchar(100) | YES |  | NULL |  
timestamp | varchar(40) | YES |  | NULL |
dom_interactive | int(11) | YES |  | NULL |
dom_loading | int(11) | YES |  | NULL |
dom_complete | int(11) | YES |  | NULL |
redirect_count | int(11) | YES |  | NULL |

<aside class="success">
We may add more performance indicators to analyize based on <code>window.performance</code>
</aside>

## User Management

Current user management is handled by NodeJS with user data stored in a local variable. Future user management will use proper password encryption using SHA256 encryption with salt.

