# AirBnB Clone Backend: Data Flow Diagram

This directory contains a Data Flow Diagram (DFD) illustrating how data moves through the AirBnB Clone backend system, focusing on key entities like users, properties, bookings, and payments.

## Repository
- **GitHub**: [alx-airbnb-project-documentation](https://github.com/AhmedNewiry/alx-airbnb-project-documentation)
- **Directory**: `data-flow-diagram/`
- **File**: `data-flow.png`

## Overview
The `data-flow.png` file is a Level-1 Data Flow Diagram created using Draw.io, mapping the flow of data for core backend operations in the AirBnB Clone system. It covers:
- **Entities**: Guest, Host, Admin, Payment Gateway.
- **Processes**: User registration/login, profile management, property creation, search, booking, payment, reviews, notifications, admin management.
- **Data Stores**: Users, Properties, Bookings, Payments, Reviews, Notifications.
- **Data Flows**: Inputs (e.g., user details, booking requests), outputs (e.g., booking confirmation, search results).

The DFD highlights data interactions for key functionalities, including user registration, property booking, and payments, as specified.

## Diagram Description
- **Title**: AirBnB Clone Backend: Level-1 Data Flow Diagram
- **Structure**:
  - **External Entities**: Guest, Host, Admin, Payment Gateway (double-border rectangles).
  - **Processes**: 9 core operations (circles, e.g., Register/Login User, Process Booking).
  - **Data Stores**: Users, Properties, Bookings, Payments, Reviews, Notifications (open-ended rectangles).
  - **Data Flows**: Arrows labeled with data (e.g., User Details, Booking Request).
- **Elements**: Blue fill for processes, green for data stores, black for entities and arrows, light gray for title.
- **Format**: PNG, A4 landscape, high resolution (300 DPI).

## How to View
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/AhmedNewiry/  alx-airbnb-project-documentation.git
   cd alx-airbnb-project-documentation/data-flow-diagram
   ```
2. **Open the PNG**:
   - Use any image viewer (e.g., Preview on macOS, Photos on Windows).
   - File: `data-flow.png`
3. **Edit the Diagram (Optional)**:
   - Import the original Draw.io file (if saved as XML) into [diagrams.net](https://app.diagrams.net/).
   - Modify and re-export as PNG if needed.

## Creation Process
1. **Tool**: Draw.io ([diagrams.net](https://app.diagrams.net/)).
2. **Steps**:
   - Created a Level-1 DFD with external entities, processes, data stores, and data flows.
   - Mapped core operations (e.g., user registration, booking, payments) based on project requirements.
   - Connected entities to processes and data stores with labeled arrows.
   - Styled with blue processes, green data stores, and black arrows for clarity.
   - Exported as `data-flow.png` (300 DPI).
3. **Storage**: Saved in `data-flow-diagram/` directory.

## Notes
- **Purpose**: Visualizes data flow for the AirBnB Clone backend, fulfilling the requirement to map key entities (users, properties, bookings, payments).
- **Alignment**: Based on features from `features-and-functionalities/` and use case diagram from `use-case-diagram/`.
- **Future Extensions**: Create Level-2 DFDs for specific processes (e.g., Process Booking) or add sequence diagrams in additional directories.
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