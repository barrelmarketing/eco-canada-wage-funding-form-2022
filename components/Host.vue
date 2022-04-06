<template>
  <div class="container p-4">
    <div id="applicant_form">
      <h1 class="fw-bold">Host Employer Application</h1>
      <div class="container-fluid mx-auto py-3 px-0" id="hostPrequalification">
        <form name="hostform" onsubmit="return false">
          <div class="card p-4 rounded bg-light mt-3">
            <h5 class="fw-bold">Organization Information</h5>
            <div class="row">
              <div class="col-lg-6 pe-5 question">
                <label for="first_name" class="form-label">First Name</label>
                <input
                  type="text"
                  class="form-control"
                  id="first_name"
                  v-model="formData.first_name"
                  placeholder="First"
                  required
                />
              </div>

              <div class="col-lg-6 pe-5 question">
                <label for="last_name" class="form-label">Last Name</label>
                <input
                  type="text"
                  class="form-control"
                  id="last_name"
                  v-model="formData.last_name"
                  placeholder="Last"
                  required
                />
              </div>

              <div class="col-lg-6 pe-5 question">
                <label for="email" class="form-label"
                  >Corporate email address</label
                >
                <input
                  type="email"
                  class="form-control"
                  id="email"
                  v-model="formData.email"
                  placeholder="name@example.com"
                  required
                />
                <div class="note">Please do not use a school email address</div>
              </div>

              <div class="col-lg-6 pe-5 question">
                <label for="job_title" class="form-label">Job Title</label>
                <input
                  type="text"
                  class="form-control"
                  id="job_title"
                  v-model="formData.job_title"
                />
              </div>

              <div class="col-lg-6 question">
                <label class="form-label"
                  >Is your company Canadian-owned or a Canadian
                  subsidiary?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="canadian_company"
                    v-model="formData.canadian_company"
                    id="canadian_company1"
                    value="Yes"
                  />
                  <label class="form-check-label" for="canadian_company1">
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="canadian_company"
                    v-model="formData.canadian_company"
                    id="canadian_company2"
                    value="No"
                  />
                  <label class="form-check-label" for="canadian_company2">
                    No
                  </label>
                </div>
              </div>
              <div class="col-lg-6 question">
                <label class="form-label"
                  >Is your application for a new employee that has not
                  previously worked in a permanent capacity?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="new_employee"
                    v-model="formData.new_employee"
                    id="new_employee1"
                    value="Yes"
                    :disabled="formData.canadian_company == 'No'"
                  />
                  <label class="form-check-label" for="new_employee1">
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="new_employee"
                    v-model="formData.new_employee"
                    id="new_employee2"
                    value="No"
                    :disabled="formData.canadian_company == 'No'"
                  />
                  <label class="form-check-label" for="new_employee2">
                    No
                  </label>
                </div>
              </div>
              <div class="col-lg-6 question">
                <label class="form-label">Organization Type:</label>
                <select
                  class="form-select form-control"
                  id="organization_type"
                  v-model="formData.organization_type"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                >
                  <option>Academia</option>
                  <option>Indigenous-Led</option>
                  <option>Not-For-Profit Organization</option>
                  <option>Micro-Industry (Less than 5 employees)</option>
                  <option>Small Industry (5-99 Employees)</option>
                  <option>Medium Industry (100-499 Employees)</option>
                  <option>Large Industry (More than 500 employees)</option>
                  <option>Utility</option>
                  <option>Municipal Government</option>
                  <option>Provincial Government</option>
                  <option>Territorial Government</option>
                </select>
              </div>
              <div class="col-lg-6 question">
                <label class="form-label">Industry Type:</label>
                <select
                  class="form-select form-control"
                  id="organization_type"
                  v-model="formData.industry_type"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                >
                  <option>Administrative and Support</option>
                  <option>Waste Management and Remediation Services</option>
                  <option>Agriculture, Forestry, Fishing and Hunting</option>
                  <option>Mining and Oil and Gas Extraction</option>
                  <option>Construction</option>
                  <option>Manufacturing</option>
                  <option>Utilities</option>
                  <option>Transportation and Warehousing</option>
                  <option>
                    Professional, Scientific, and Technical Services
                  </option>
                  <option>Public Administration</option>
                  <option>Wholesale Trade/Retail Trade</option>
                  <option>Information and Cultural Industries</option>
                  <option>
                    Finance and Insurance, Real Estate and Rental and Leasing
                  </option>
                  <option>Management and Companies and Enterprises</option>
                  <option>
                    Arts, Entertainment and Recreation, Accomodation and Food
                    Services
                  </option>
                  <option>Other Services (except Public Administration)</option>
                </select>
              </div>
              <div class="col-lg-6 question">
                <label class="form-label"
                  >Why is your organization applying for wage funding?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="reason_for_applying"
                    v-model="formData.reason_for_applying"
                    id="reason_for_applying1"
                    value="Won a new project"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="reason_for_applying1">
                    Won a new project
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="reason_for_applying"
                    v-model="formData.reason_for_applying"
                    id="reason_for_applying2"
                    value="Launching a new program or business stream"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="reason_for_applying2">
                    Launching a new program or business stream
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="reason_for_applying"
                    v-model="formData.reason_for_applying"
                    id="reason_for_applying3"
                    value="Adapting to green sustainability initiatives"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="reason_for_applying3">
                    Adapting to green sustainability initiatives
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="reason_for_applying"
                    v-model="formData.reason_for_applying"
                    id="reason_for_applying4"
                    value="Entering into a new industry "
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="reason_for_applying4">
                    Entering into a new industry
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="reason_for_applying"
                    v-model="formData.reason_for_applying"
                    id="reason_for_applying5"
                    value="Organization Growth"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="reason_for_applying5">
                    Organization Growth
                  </label>
                </div>
              </div>
              <div class="col-lg-6 question">
                <label class="form-label"
                  >How many employees work for your company?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="number_of_employees"
                    id="number_of_employees1"
                    value="Less than 5"
                    v-model="formData.number_of_employees"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="number_of_employees1">
                    Less than 5
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="number_of_employees"
                    id="number_of_employees2"
                    value="5-99"
                    v-model="formData.number_of_employees"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="number_of_employees2">
                    5-99
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="number_of_employees"
                    id="number_of_employees3"
                    value="100-499"
                    v-model="formData.number_of_employees"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="number_of_employees3">
                    100-499
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="number_of_employees"
                    id="number_of_employees4"
                    value="More than 500"
                    v-model="formData.number_of_employees"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="number_of_employees4">
                    More than 500
                  </label>
                </div>
              </div>
            </div>
          </div>

          <div class="card p-4 rounded bg-light mt-5">
            <h5 class="card-title fw-bold">Address Information</h5>

            <div class="row">
              <div class="col-lg-6 question">
                <label for="streetAddress" class="form-label"
                  >Street Address</label
                >
                <input
                  type="text"
                  class="form-control"
                  id="streetAddress"
                  v-model="formData.street_address"
                  placeholder="Business Address"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                />
              </div>

              <div class="col-lg-6 question">
                <label for="city" class="form-label">City</label>
                <input
                  type="text"
                  class="form-control"
                  id="city"
                  v-model="formData.city"
                  placeholder="City"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                />
              </div>
              <div class="col-lg-6 question">
                <label for="province" class="form-label">Province</label>
                <select
                  id="province"
                  class="form-control form-select"
                  v-model="formData.province"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                >
                  <option selected disabled value="">Select Province</option>
                  <option value="AB">Alberta</option>
                  <option value="BC">British Columbia</option>
                  <option value="MB">Manitoba</option>
                  <option value="NB">New Brunswick</option>
                  <option value="NL">Newfoundland and Labrador</option>
                  <option value="NS">Nova Scotia</option>
                  <option value="ON">Ontario</option>
                  <option value="PE">Prince Edward Island</option>
                  <option value="QC">Quebec</option>
                  <option value="SK">Saskatchewan</option>
                  <option value="NT">Northwest Territories</option>
                  <option value="NU">Nunavut</option>
                  <option value="YT">Yukon</option>
                </select>
              </div>
              <div class="col-lg-6 question">
                <label for="postal_code" class="form-label">Postal Code</label>
                <input
                  type="text"
                  class="form-control"
                  id="postal_code"
                  placeholder="Postal Code"
                  :disabled="
                    formData.canadian_company == 'No' ||
                    formData.new_employee == 'No'
                  "
                />
              </div>
            </div>
          </div>

          <div class="card p-4 rounded bg-light mt-5">
            <h5 class="card-title fw-bold">Position Information</h5>

            <div class="row">
              <div class="col-12 question" id="imm_role_question">
                <label class="form-label"
                  >This is a full-time position within your organization geared
                  towards skilled immigrants attempting to enter the Canadian
                  environmental workforce.
                </label>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="imm_role"
                    v-model="formData.imm_role"
                    id="imm_role1"
                    value="Yes"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="imm_role1"> Yes </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="imm_role"
                    v-model="formData.imm_role"
                    id="imm_role2"
                    value="No"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="imm_role2"> No </label>
                </div>
              </div>
              <div class="col-12 question" id="permanent_role_question">
                <label class="form-label"
                  >This position is for a full-time permanent position within
                  your organization.
                </label>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="permanent_role"
                    v-model="formData.permanent"
                    id="permanent_role1"
                    value="Yes"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="permanent_role1">
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="permanent_role"
                    v-model="formData.permanent"
                    id="permanent_role2"
                    value="No"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label" for="permanent_role2">
                    No
                  </label>
                </div>
              </div>
              <div class="col-12 question" id="coop_question">
                <label class="form-label"
                  >This position is for a paid student work integrated learning
                  opportunity related to the environment or an environmental
                  project in STEAM (Science, Technology, Engineering, Arts,
                  Mathematics) or Business.
                </label>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="coop_role"
                    v-model="formData.steam_position"
                    id="coop_role1"
                    value="Yes"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No' ||
                      formData.permanent == 'Yes'
                    "
                  />
                  <label class="form-check-label" for="coop_role1"> Yes </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="coop_role"
                    v-model="formData.steam_position"
                    id="coop_role2"
                    value="No"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No' ||
                      formData.permanent == 'Yes'
                    "
                  />
                  <label class="form-check-label" for="coop_role2"> No </label>
                </div>
              </div>
            </div>
          </div>

          <div
            class="card p-4 rounded bg-light mt-5"
            v-if="formData.permanent == 'Yes' && formData.imm_role !== 'Yes'"
            :imm-role="formData.imm_role"
          >
            <h5 class="fw-bold">Finding the best fit</h5>
            <h6>
              Please select the option that aligns best with the role you are
              applying for:
            </h6>

            <div class="row">
              <div
                :class="
                  'col-11 permanent_role_option ds4y' +
                  (formData.number_of_employees == 'More than 500'
                    ? ' disabled'
                    : '')
                "
              >
                <div class="form-check d-block">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="job_role"
                    id="job_role1"
                    value="DS4Y"
                    v-model="formData.chosen_program"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No' ||
                      formData.number_of_employees == 'More than 500'
                    "
                  />
                  <label class="form-check-label pl-3" for="job_role1">
                    This position fits in <b>Digital Skill</b> <br /><br />
                    <h6>Example roles:</h6>
                    <ul class="list">
                      <li>Coding and app development</li>
                      <li>Software development</li>
                      <li>GIS analysis</li>
                      <li>Adaptive technologies</li>
                      <li>Network troubleshooting</li>
                      <li>Website development</li>
                      <li>Web-enabled learning</li>
                      <li>
                        Social media campaigns and other content development
                      </li>
                    </ul>
                  </label>
                </div>
                <div
                  class="note fw-bold"
                  name="failure"
                  style="line-height: 1.15rem"
                  id="ds4y_failure"
                  v-if="formData.number_of_employees == 'More than 500'"
                >
                  Unfortunately, only companies with fewer than 500 employees
                  are eligible for Digital Skills 4 Youth.
                </div>
              </div>
              <div class="col-11 permanent_role_option shi">
                <div class="form-check d-block">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="job_role"
                    id="job_role2"
                    value="STEAM"
                    v-model="formData.chosen_program"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label pl-3" for="job_role2">
                    This position fits in
                    <b
                      >Science, Technology, Engineering, Arts, Math (STEAM) &
                      Business</b
                    >
                    <br /><br />
                    <h6>Example roles:</h6>
                    <ul>
                      <li>
                        Physical Science Professionals
                        <ul>
                          <li>Chemists</li>
                          <li>Geologists, Geochemists & Geophysicists</li>
                          <li>Meteorolgists</li>
                          <li>Physicists & Astronomers</li>
                          <li>Other</li>
                        </ul>
                      </li>
                      <li>
                        Technical Occupation in Physical Science
                        <ul>
                          <li>Chemical Technologists & Technicians</li>
                          <li>
                            Geological & Mineral Technologists & Technicians
                          </li>
                          <li>Meteorolgical Technicians</li>
                          <li>Other</li>
                        </ul>
                      </li>
                      <li>
                        Life Science Professionals
                        <ul>
                          <li>
                            Agricultural Representatives, Consultants &
                            Specialists
                          </li>
                          <li>Biologists & Related Scientists</li>
                          <li>Forestry Professionals</li>
                          <li>Other</li>
                        </ul>
                      </li>
                      <li>
                        Technical Occupation in Life Sciences
                        <ul>
                          <li>Agricultural & Fish Product Inspectors</li>
                          <li>Biological Technologists & Technicians</li>
                          <li>Conservation & Fishery Officers</li>
                          <li>Forestry Technologists & Technicians</li>
                          <li>
                            Landscape & Horticulture Technicians & Specialists
                          </li>
                          <li>Other</li>
                        </ul>
                      </li>
                    </ul>
                  </label>
                </div>
              </div>
              <div class="col-11 permanent_role_option ynr">
                <div class="form-check d-block">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="job_role"
                    id="job_role3"
                    value="YNR"
                    v-model="formData.chosen_program"
                    :disabled="
                      formData.canadian_company == 'No' ||
                      formData.new_employee == 'No'
                    "
                  />
                  <label class="form-check-label pl-3" for="job_role3">
                    This position fits in <b>Natural Resources</b> <br /><br />
                    <em>Example roles:</em>
                    <ul>
                      <li>
                        Energy
                        <ul>
                          <li>
                            Non-renewable Energy (eg. Oil and gas extraction,
                            support services, refining, pipelines)
                          </li>
                          <li>
                            Renewable and Non-Emitting Technologies (eg Solar,
                            wind, hydro nuclear, carbon capture biofuels)
                          </li>
                          <li>
                            Electricity, Transmission and Distribution (eg Other
                            electrical generation, Smart grid, energy storage)
                          </li>
                          <li>
                            Energy Efficient (eg. Retrofits, HVAC, green
                            buildings, cogeneration)
                          </li>
                        </ul>
                      </li>
                      <li>
                        Forest Sector
                        <ul>
                          <li>Forestry and Support Activities</li>
                          <li>Wood Product Manufacturing</li>
                          <li>Pulp and Paper Product Manufacturing</li>
                        </ul>
                      </li>
                      <li>
                        Mining and Minerals
                        <ul>
                          <li>
                            Junior Mining (eg Mineral exploration, including
                            critical minerals and metals used in advanced
                            manufacturing, renewable energy clean technologies)
                          </li>
                          <li>
                            Senior Mining (eg. Operating mines, developing
                            mining project, process and refining or minerals and
                            metals)
                          </li>
                          <li>
                            Mining Supply and Services (eg Form that provide
                            goods and services purchased by mining companies,
                            large firms, and revenue generating OEM’s, research
                            organizations, clean technologies.)
                          </li>
                          <li>Mine Reclamation and Closure</li>
                          <li>Mining Value from Waste</li>
                        </ul>
                      </li>
                      <li>
                        Earth Sciences
                        <ul>
                          <li>
                            Environmental Assessment and Environmental
                            Protection
                          </li>
                          <li>
                            Geology and Geoscience (eg. Soil and water testing
                            surveying, hydrography, geo-mapping, remote sensing)
                          </li>
                          <li>Natural Hazards</li>
                          <li>Climate Change Adaptation</li>
                        </ul>
                      </li>
                    </ul>
                  </label>
                </div>
              </div>
            </div>
          </div>
          <button
            type="submit"
            v-if="!submit"
            id="submitPrequalification"
            class="btn my-4 w-100 btn-success shadow-sm rounded-0"
            :disabled="!formComplete || submit == true"
            @click="finishQuiz"
            v-html="loadingText"
          ></button>
          <!-- Response Section -->
          <div class="col my-3" v-if="submit">
            <Qualified
              id="IMM_thankyou"
              link="#"
              text="
              Thank you for your interest in funding from our Employment
              Programs. Based on your answers in the pre-qualification form,
              this role aligns with our Job readiness Program for Highly Skilled Immigrants in the Environmental Sector.
              Please click the button below to start your application."
              v-if="
                (formData.steam_position == 'No' &&
                  formData.permanent == 'Yes') ||
                (formData.permanent == 'Yes' && formData.imm_role == 'Yes')
              "
            />
            <Qualified
              id="ds4y_thankyou"
              link="#"
              text="
              Thank you for your interest in funding from our Employment
              Programs. Based on your answers in the pre-qualification form,
              this role aligns with our Digital Skills 4 Youth (DS4Y) Program.
              Please click the button below to start your application."
              v-if="
                (formData.steam_position == 'No' &&
                  formData.permanent == 'Yes') ||
                (formData.permanent == 'Yes' &&
                  formData.chosen_program == 'DS4Y')
              "
            />

            <Qualified
              id="ynr_thankyou"
              link="#"
              text="Thank you for your interest in funding from our Employment
              Programs. Based on your answers in the pre-qualification form,
              this role aligns with our Youth Employment in Natural Resources
              (YNR) Program. Please click the button below to start your
              application."
              v-if="
                (formData.steam_position == 'No' &&
                  formData.permanent == 'Yes') ||
                (formData.permanent == 'Yes' &&
                  formData.chosen_program == 'YNR')
              "
            />

            <Qualified
              id="shi_thankyou"
              link="#"
              text="Thank you for your interest in funding from our Employment
              Programs. Based on your answers in the pre-qualification form,
              this role aligns with our SHI Program. Please click the button
              below to start your application."
              v-if="
                (formData.steam_position == 'No' &&
                  formData.permanent == 'Yes') ||
                (formData.permanent == 'Yes' &&
                  formData.chosen_program == 'STEAM')
              "
            />

            <Qualified
              id="studentCoopHost"
              link="#"
              text="Thank you for your interest in funding from our Employment
              Programs. Based on your answers in the pre-qualification form,
              this role aligns with our Co-op Student Work Placement Program.
              Please click the button below to start your application."
              v-if="
                formData.steam_position == 'Yes' && formData.permanent == 'No'
              "
            />

            <Disqualified
              v-if="
                (submit &&
                  formData.steam_position == 'No' &&
                  formData.permanent == 'No') ||
                (formData.new_employee == 'No' &&
                  formData.canadian_company == 'Yes')
              "
              message='Thank you for your interest in our Employment Programs.
              Unfortunately, your answers in do not
              align with our offerings at this time. Please check out our HR resources
              <a href="/new-practitioners/employment-support/job-board/"
                >Job Board with AI-matching</a
              > to help you in your recruitment efforts.'
            />
          </div>

          <!-- Error Section -->
          <div
            class="note conditional p-4 border text-center"
            id="testCitizenship"
            v-show="notCanadianCompany"
          >
            <h6>
              Thank you for your interest.
              <br /><br />
              Permanent, full-time funding
              <b>is only available for Canadian Organizations</b>.
            </h6>
          </div>
        </form>
      </div>
    </div>
    <div id="debugPanel">
      <pre>{{ formData }}</pre>
      <pre>submit: {{ submit }}</pre>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import Disqualified from "./Disqualified.vue";
export default {
  components: { Disqualified },
  data() {
    return {
      submit: false,
      loading: false,

      formData: {
        first_name: "s",
        last_name: "p",
        email: "s@p.ca",
        employment: "",
        coop: "",
        permanent: "",
        imm_role: "",
        steam_position: "",
        job_title: "",
        canadian_company: "",
        new_employee: "",
        reason_for_applying: "",
        number_of_employees: "",
        street_address: "",
        city: "",
        province: "",
        chosen_program: "",
      },
    };
  },
  computed: {
    tooOld() {
      if (
        moment(this.formData.birth_date).year() > 1900 &&
        this.formData.birth_date.length == 10
      ) {
        let ageLimit = moment().subtract(31, "years").format("YYYY-MM-DD");
        return moment(this.formData.birth_date).isBefore(ageLimit, "day");
      } else {
        return false;
      }
    },
    notCanadianCompany() {
      if (this.formData.canadian_company == "No") {
        return true;
      } else {
        return false;
      }
    },
    formComplete() {
      if (
        this.formData.first_name &&
        this.formData.last_name &&
        this.formData.email &&
        this.formData.canadian_company == "Yes" &&
        this.formData.new_employee == "Yes"
      ) {
        return true;
      } else {
        return false;
      }
    },
    loadingText() {
      if (this.loading) {
        return "Checking eligibility...";
      } else {
        return "Check Funding Eligibility";
      }
    },
  },
  methods: {
    finishQuiz() {
      let vm = this;
      this.loading = true;
      setTimeout(function () {
        vm.submit = true;
        vm.loading = false;
      }, 1000);
    },
  },
  mounted() {
    window.formData = this.formData;
  },
};
</script>

<style>
</style>