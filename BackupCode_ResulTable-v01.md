import React, { useState } from "react";

const UniversityAccordion = ({ universities = [] }) => {
  const [openIndex, setOpenIndex] = useState(null);

  const toggleAccordion = (index) => {
    setOpenIndex(openIndex === index ? null : index);
  };

  return (
    <div style={{ marginTop: "30px", width: "100%" }}>
      {universities.map((uni, index) => {
        const matchedCourses = Array.isArray(uni.courses) ? uni.courses : [];

        return (
          <div
            key={index}
            style={{
              border: "1px solid #ccc",
              borderRadius: "8px",
              marginBottom: "16px",
              background: "#f9f9f9",
            }}
          >
            <div
              onClick={() => toggleAccordion(index)}
              style={{
                cursor: "pointer",
                padding: "16px",
                fontWeight: "bold",
                fontSize: "18px",
              }}
            >
              {openIndex === index ? "▾" : "▸"} {uni.partner_university} ({uni.country})
            </div>

            {openIndex === index && (
              <div style={{ padding: "16px", background: "#fff" }}>
                {matchedCourses.length === 0 ? (
                  <p>No course mappings available.</p>
                ) : (
                  <table style={{ width: "100%", borderCollapse: "collapse" }}>
                    <thead>
                      <tr style={{ backgroundColor: "#FF671D", color: "white" }}>
                        <th style={tableHeaderStyle}>Class Code</th>
                        <th style={tableHeaderStyle}>Course Title</th>
                        <th style={tableHeaderStyle}>UOP Equivalent Code</th>
                        <th style={tableHeaderStyle}>Expiration</th>
                      </tr>
                    </thead>
                    <tbody>
                      {matchedCourses.map((course, i) => (
                        <tr key={i}>
                          <td style={tableCellStyle}>{course.partner_course_code}</td>
                          <td style={tableCellStyle}>{course.partner_course_name}</td>
                          <td style={tableCellStyle}>{course.pacific_course_code}</td>
                          <td style={tableCellStyle}>{course.approval_term || "N/A"}</td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                )}
              </div>
            )}
          </div>
        );
      })}
    </div>
  );
};

const tableHeaderStyle = {
  padding: "10px",
  textAlign: "left",
  fontWeight: "bold",
};

const tableCellStyle = {
  padding: "10px",
  borderBottom: "1px solid #ccc",
};

export default UniversityAccordion;
