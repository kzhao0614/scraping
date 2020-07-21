library(rvest)

##Establish Login Page URL
login <- "https://imaginela.nationbuilder.com/forms/user_sessions/new" 

##Create html session and login with credentials
pgsession <- html_session(login)
pgform <- html_form(pgsession)[1]
filled_form <- set_values(pgform[[1]], 'user_session[email]' = "kevinrihuazhao@gmail.com", 'user_session[password]' = "June222020")
submit_form(pgsession, filled_form)

##Scraping activity page for data
url <- "https://imaginela.nationbuilder.com/admin/streams/activity?type_id=&range=All%20time&as_page=1"
activity <- jump_to(pgsession, url)
description <- html_nodes(activity, css = ".activity-description") ####Function cannot find the information under this divider, this part breaks
description 

html_text(html_nodes(description, "span"))
