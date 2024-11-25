# STRICT GUIDELINES

Please read these guildelines thoroughly. These guidelines are non-negotiable and must be adhered to without exception.

## Communication (Slack)

- Submit daily progress reports promptly at the beginning and end of each day.
- Immediate notification of any blockers or challenges is mandatory.
  - Our team is available to assist, ensuring swift resolution (We work as team).
- Proactively communicate any delays in milestone deadlines.
  - Failure to do so will not be tolerated.

## Task Management (Asana)

- All projects must be meticulously broken down into smaller tasks/subtasks.
  - Specify estimated completion times for every task.
- Ensure tasks include adequate time for research, implementation, testing, documentation, etc.

## GitHub

- Each bugfix or feature requires its own PR.
- Base all PRs on the master/main branch by default.
- Code must be pushed to GitHub at the end of each day, regardless of completeness.
- Again, Code must be pushed to GitHub at the end of each day, regardless of completeness.
- All commented or unused code must be removed before submitting a PR, with justification if necessary.

## Coding

- Follow a consistent coding style throughout the project for uniformity.
- Prioritize code efficiency and optimization to enhance performance.
- Emphasize code readability and maintainability through clear and descriptive comments.

## Validation

- Most of the user input must be validated.
- Validation needs to be done in the backend and mirrored to the frontend using [Laravel Precognition](https://laravel.com/docs/11.x/precognition).
- Custom validation rules should follow the structure outlined in the [Laravel documentation](https://laravel.com/docs/validation#custom-validation-rules)

## Tests

- A new test must accompany each feature.
- Ensure 100% coverage of class functionality. (https://github.com/FmTod2/pestphp-docker)
- Create missing tests for existing classes when working on bugfixes/changes.
- Implement GitHub actions to run tests in both Windows and Linux environments.

## Documentation
- Provide comprehensive documentation for each new implementation or code addition.
- Ensure all documentation is written in Markdown format.
- Include a diagram illustrating the overall flow of the added functionality, covering both backend and frontend aspects.

## Naming Conventions

- Adhere strictly to existing naming conventions in ongoing projects.
- Select and consistently apply a naming convention for new projects.

## Laravel ([Read More](./PHP.md))

- Prioritize Laravel's methodologies over vanilla PHP conventions for consistency and efficiency.
- Steer clear of duplicating functionality that is readily available within the framework.
