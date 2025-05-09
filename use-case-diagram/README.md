# AirBnB Clone Backend: Use Case Diagram

This directory contains a use case diagram visualizing the interactions between users and the AirBnB Clone backend system for key functionalities, including user registration, property booking, and payments.

## Repository
- **GitHub**: [alx-airbnb-project-documentation](https://github.com/AhmedNewiry/alx-airbnb-project-documentation)
- **Directory**: `use-case-diagram/`
- **File**: `airbnb-use-case-diagram.png`

## Overview
The `airbnb-use-case-diagram.png` file is a UML use case diagram created using Draw.io, illustrating how actors (Guest, Host, Admin) interact with the AirBnB Clone backend system. It covers the following core functionalities:
- User Management (registration, login, profile updates)
- Property Listings Management (create/edit/delete listings)
- Search and Filtering (search properties by location, price, etc.)
- Booking Management (book properties, cancel bookings, track status)
- Payment Integration (make payments, receive payouts)
- Reviews and Ratings (leave reviews, respond to reviews)
- Notifications System (email/in-app notifications)
- Admin Dashboard (manage users, listings, bookings, payments)

The diagram captures all key actors and their interactions with the system, emphasizing user registration, property booking, and payments as specified.

## Diagram Description
- **Title**: AirBnB Clone Backend: Use Case Diagram
- **Structure**:
  - **Actors**: Guest, Host (left), Admin (right).
  - **System Boundary**: AirBnB Clone Backend System.
  - **Use Cases**: Ovals for functionalities (e.g., Register, Book Property), grouped by category (e.g., User Management, Booking Management).
  - **Relationships**: Solid lines for actor-use case associations, dashed lines for include/extend relationships (e.g., Login includes Authenticate).
- **Elements**: Stick figures for actors, ovals for use cases, blue fill for use cases, light gray for title.
- **Format**: PNG, A4 landscape, high resolution (300 DPI).

## How to View
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/AhmedNewiry/alx-airbnb-project-documentation.git
   cd alx-airbnb-project-documentation/use-case-diagram
   ```
2. **Open the PNG**:
   - Use any image viewer (e.g., Preview on macOS, Photos on Windows).
   - File: `airbnb-use-case-diagram.png`
3. **Edit the Diagram (Optional)**:
   - Import the original Draw.io file (if saved as XML) into [diagrams.net](https://app.diagrams.net/).
   - Modify and re-export as PNG if needed.

## Creation Process
1. **Tool**: Draw.io ([diagrams.net](https://app.diagrams.net/)).
2. **Steps**:
   - Created a UML use case diagram with a system boundary and actors (Guest, Host, Admin).
   - Added use cases as ovals, grouped by functionality (e.g., User Management, Booking Management).
   - Connected actors to use cases with solid lines and used dashed lines for include/extend relationships.
   - Styled with blue fill for use cases, black lines, and a light gray title.
   - Exported as `airbnb-use-case-diagram.png` (300 DPI).
3. **Storage**: Saved in `use-case-diagram/` directory.

## Notes
- **Purpose**: Visualizes system interactions for the AirBnB Clone backend, fulfilling the requirement to capture key functionalities like user registration, property booking, and payments.
- **Alignment**: Based on the project requirements, covering all core functionalities and key actors.
- **Future Extensions**: Add sequence diagrams or activity diagrams in additional directories to complement this use case diagram.
- **Repository**: Ensure the `alx-airbnb-project-documentation` repository is initialized before committing.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-feature`.
3. Commit changes: `git commit -m "Add your feature"`.
4. Push: `git push origin feature/your-feature`.
5. Open a pull request.

For issues, open an issue on GitHub.

## Contact
Contact maintainers via GitHub issues.

---