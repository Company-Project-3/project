This is a complete documentation of the processes needed for creating a custom windows image.

## Task Sequences
Task sequence is a set of actions excuted in a linear order.

#### Create a new Task Sequence.
1. ![alt text](<Screenshot 2024-04-24 142617.png>)
- Input task ID sequence ID
- Input task seqence name
- input sequence comments(if any)
- Select the next icon

2. ![alt text](<Screenshot 2024-04-24 144308.png>)
- Select the Standard Client Task Sequence template.
- select the next icon

3. ![alt text](<Screenshot 2024-04-24 145319.png>)
- Select the needed opearting system.
- select the next icon

4. ![alt text](<Screenshot 2024-04-24 145619.png>)
- Specify a product key if applicable, for this task we opted for the **do not specify product key at this time** option.


5. ![alt text](<Screenshot 2024-04-24 151139.png>)
- Specify OS settings.
    - Add the Full name
    - Add your Organization
    - Add default browser page.
- Select the next icon

6. ![alt text](<Screenshot 2024-04-24 151537.png>)
- Specify the local admin password for the task sequence if applicable.
- Select the next icon

7. ![alt text](<Screenshot 2024-04-24 151608.png>)
- Confirm your selections in the summary
- Select the next icon
- Select the finish icon

8. ![alt text](<Screenshot 2024-04-24 151759.png>) 
- Select the created task sequence and navigate to the properties page.
- Leave the general tab on the default settings page

**NOTE:** IF you have many task sequences you can disable the one that is not needed by toggling **the Enable this task sequence option**.
- Select the task sequence tab

9. ![alt text](<Screenshot 2024-04-24 151819.png>)
- On the task sequence page, you can toogle between each steps to activate or de-activate certain tasks.
- Expand the state restore option and select the windows update (pre-application installation), navigate to the options menu and tick the **Disable this step** option and apply changes
- Select the windows update (post-application installation), navigate to the options menu and tick the **Disable this step** option and apply changes.
- Select the OK icon.
