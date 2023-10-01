# Week 4: Code Review

## Code Review Challenge

For this week's portfolio entry, I chose to review the code 'The Big Boss', a code snippet that exhibited the "Middle Man" code smell. 

In the initial code, the `Person` class acted as a middleman, merely delegating the `GetManager` call to the `Department` class. 

### Initial Code

```csharp
class HumanResources
{
    static void Main(string[] args)
    {
        Person person = new Person();
        person = person.GetManager();
    }
}

class Person
{
    public Department Department { get; set; }
    public Person GetManager()
    {
        return Department.GetManager();
    }
}

class Department
{
    private readonly Person _manager;
    public Department(Person manager)
    {
        _manager = manager;
    }
    public Person GetManager()
    {
        return _manager;
    }
}
```

### Suggested fix

```csharp
class HumanResources
{
    static void Main(string[] args)
    {
        Department department = new Department();
        Person manager = department.GetManager();
    }
}

class Department
{
    private readonly Person _manager;
    
    public Department()
    {
        _manager = new Person(); 
    }

    public Person GetManager()
    {
        return _manager;
    }
}

```
### Analysis
As mentioned, the initial code exhibited the "Middle Man" code smell, where the Person class acted as an unnecessary intermediary. I, therefore, eliminated the Person class as a middleman and directly instantiated a Department object to get the manager. This simplifies the code, removes unnecessary complexity, and adheres to the principle of avoiding middleman classes when they don't add value.

I believe it is safe to say then, that with my fix, it's now clear that we're getting the manager directly from the `Department` class. There are fewer unnecessary steps and objects involved, enhancing the code's clarity and readability.

![Middle Man](images/middle_man.png)
<br>

*Figure 1: Middle Man Representation. Taken from [RefactoringGuru](https://refactoring.guru/smells/middle-man)*

### Code Review in the team
Thanks to these challenges, I was able to provide a good Code Review for one of my teammates. This week, we were able to complete some code reviews

![Code Review Team](images/CodeReviewTeam.png)
<br>

*Figure 2: Code Review in the team*