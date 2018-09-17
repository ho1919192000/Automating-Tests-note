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

Example: 

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
