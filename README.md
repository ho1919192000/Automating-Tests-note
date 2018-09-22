# Automating-Tests-note
Note of "The Way of the Web Tester. A Beginner's Guide to Automating Tests"
## The Testing Pyramid
### UI Tests: The user interface tests test the application from the UI layer down
 - Go end-to-end
 - See what a user would see
 - Expensive & slow

### Integration Tests: Intergration tests, on the other hand, don't go through the UI.
 - Web services & APIs
 - Connectivity
 - Not most precise

### Unit Test: For precision, speed, and coverge, we rely on unit tests.
 - Lightning fast
 - Extremely versatile
 - Miss integration

### Rules of Thumb 
 1. Favor unit tests over UI.
 2. Cover unit test gaps with integration tests.
 3. Use UI tests sparingly.
## The Smoking User Interface
### Enter the User Interface Test
User Interface test (or UI) are scripts that test your application in the same way an end user would.
### What UI test tell us?
- Our application are correctly deployed
- Our environment are correctly configured
- All the pieces of our architecture are connected and hooked up right

Example  

steps to log in:
1. visit login page
2. fill in email address
3. fill in password
4. click sign-in button
5. check for presence of 'Weclome'
```Ruby
describe 'should be able to login' do
 let(:user) {FactoryGirl.create(:user)}
 before do
  visit login_path
  fill_in 'Email' with: user.password
  click_button 'Sign in'
 end
 it {should have_selector('h1',text: 'Welcome')}
end
```
### Grap certain element
```JavaScript
$("input[type=text]")[0]
//OR
$("#email")
```
## Chapter 4 Connecting the Dots with Intergration Tests
### How the Web Works?
1. Click and URL: http://funnycatz.com/piano.html
2. A lookup service called DNS(Domain Name System) take part of that URL and convert it into an IP address
3. Browser take IP address and create the URL necessaty to fullfill user request.  
http://funnycatz.com/piano.html -> DNS -> http://192.168.1.1:80/piano.html  
http://192.168.1.1:80/piano.html  
Protocol     IP   Port    Resource  
**Port:** Port numbers are the channels that servers are listening for incoming requests on. By default is usually port 80, but it could be anything(like 3000 or 8080)  
### Talking HTTP
**REST** stands for representational state transfer, is one of style to design web APIs.  
- URL: resources we are looking for  
**Main Four Verbs**  
HTTP GET: Read (ex: /photo/:id) for getting existing resources  
HTTP POST: Create (ex: /photos) for creating new one  
HTTP PUT: Update (ex: /photo/:id) for updating existing resources  
HTTP DELETE: Delete (ex: /photo/:id) for deleting existing ones  
## Chapter 5 Integration Testing RESTful Web Service  
### CRUD  
Get(read)  
Post(create)  
Put(update)  
Delete(delete) 
## Common Status Code
**Code  Meaning&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Description**  
200 Success Everything worked OK  
302 Redirect You are being redirected to another page  
404 Missing We couldn't find what you were looking for  
500 Error Something went wrong on our end  
## HTTP GET
```Ruby
def setup
  @permit = permits(:saskatoon)
end

test 'HTTP GET' do
  get permit_path(:id => @permit.id, :format => :json)
  assert response.body.to_s.include? 'Saskatoon'
  assert_response :success # 200 ok
 end
```
## HTTP POST
```Ruby
test 'HTTP POST' do
  permit = Permit.find_by_location('Moose Jaw')
  #verify it doesn't exist
  assert_nil permit
  #create it
  post permits_path, permit: {location: 'Moose Jaw'}
  #search for it again
  permit = Permit.find_by_location('Moose Jaw')
  #verify was created
  assert_not_nil permit
  #check_response :redirect
 end 
```
## HTTP PUT
```Ruby
test 'HTTP PUT' do
  #search for permit by new attribute
  permit = Permit.find_by_location('Medicine Hat')
  #verify it doesn't exist
  assert_nil permit
  #update it
  put permits_path(@permit), permit: {location: 'Medicine Hat'}
  #search for it again
  permit = Permit.find_by_location('Medicine Hat')
  #verify was created
  assert_not_nil permit
  #check response 
  assert_response :redirect
 end 
```
## HTTP DELETE
```Ruby
test 'HTTP DELETE' do
 delete permit_pate(@permit)
 assert_response : redirect
 
 assert_raises(ActiveRecord::RecordNotFound) do
   get permit_path(@permit)
   end
end
```
