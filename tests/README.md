# Tests

> **Showcase edition:** this is documentation for the private implementation. Source, runtime dependencies, and model weights are not included here. Commands require the full private checkout. [Repository scope](../SOURCE_ACCESS.md).

Tests are grouped by responsibility: `backend/`, `simulation/`, `training/`, and
`ros2/`. Run `python -m pytest -q` from the repository root. Frontend tests live
in `frontend/src/tests/` and run with `npm --prefix frontend test`.

ROS tests inspect package and model definitions; they do not launch Gazebo.
