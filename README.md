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
