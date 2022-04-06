<template>
  <div class="container p-4">
    <div id="applicant_form">
      <h1 class="fw-bold">Job-Seeker Application Form</h1>
      <div
        class="container-fluid mx-auto py-3 px-0"
        id="candidatePrequalification"
      >
        <form name="applicantform" onsubmit="return false">
          <div class="card p-4 rounded bg-light mt-3">
            <h5 class="fw-bold">Personal Information</h5>
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
                  >Personal email address</label
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
                <label for="dob" class="form-label">Date of Birth</label>
                <input
                  type="date"
                  class="form-control"
                  id="dob"
                  v-model="formData.birth_date"
                  required
                />
              </div>
            </div>
          </div>

          <div class="card p-4 rounded bg-light mt-5">
            <h5 class="card-title fw-bold">Finding the Right Program</h5>

            <div class="row">
              <div
                class="col-lg-6 pe-5 question"
                :data-status="formData.citizenship"
              >
                <label class="form-label"
                  >What is your current Canadian Citizenship Status?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="citizenship"
                    v-model="formData.citizenship"
                    id="citizenship1"
                    value="Canadian Citizenship"
                  />
                  <label class="form-check-label" for="citizenship1">
                    Canadian Citizen
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="citizenship"
                    id="citizenship2"
                    v-model="formData.citizenship"
                    value="Permanent Resident"
                  />
                  <label class="form-check-label" for="citizenship2">
                    Permanent Resident
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="citizenship"
                    id="citizenship3"
                    v-model="formData.citizenship"
                    value="Refugee"
                  />
                  <label class="form-check-label" for="citizenship3">
                    Refugee
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="citizenship"
                    id="citizenship4"
                    v-model="formData.citizenship"
                    value="New Immigrant"
                  />
                  <label class="form-check-label" for="citizenship4">
                    New Immigrant
                  </label>
                </div>
              </div>

              <div class="col-lg-6 pe-5 question">
                <label class="form-label"
                  >What is your current Employment Status?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="employment"
                    id="employment1"
                    v-model="formData.employment"
                    value="Student"
                  />
                  <label class="form-check-label" for="employment1">
                    Student
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="employment"
                    id="employment2"
                    v-model="formData.employment"
                    value="Recent or Soon to Graduate"
                  />
                  <label class="form-check-label" for="employment2">
                    Recent or Soon to Graduate
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="employment"
                    id="employment3"
                    v-model="formData.employment"
                    value="Graduated and Unemployed"
                    @click="formData.coop = 'No'"
                  />
                  <label class="form-check-label" for="employment3">
                    Graduated and Unemployed
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="employment"
                    id="employment4"
                    v-model="formData.employment"
                    value="Graduated and Underemployed"
                    @click="formData.coop = 'No'"
                  />
                  <label class="form-check-label" for="employment4">
                    Graduated and Underemployed
                  </label>
                </div>
              </div>
            </div>
          </div>

          <div class="card p-4 rounded bg-light mt-5" v-show="!notCitizen">
            <h5 class="fw-bold">What type of program are you looking for?</h5>

            <div class="row">
              <div class="col-lg-6 pe-5 question">
                <label
                  :class="
                    'form-label' +
                    (formData.employment.includes('employed')
                      ? ' text-muted'
                      : ' ')
                  "
                  >Are you looking for a co-op position related to the
                  environment or working on environmental projects?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="coop"
                    id="coop1"
                    v-if="!formData.employment.includes('employ')"
                    v-model="formData.coop"
                    value="Yes"
                    :disabled="formData.employment.includes('employed')"
                  />
                  <label
                    v-if="!formData.employment.includes('employ')"
                    class="form-check-label"
                    for="coop1"
                  >
                    Yes
                  </label>
                  <input
                    class="form-check-input"
                    type="radio"
                    name="coop"
                    id="coop1"
                    v-if="formData.employment.includes('employ')"
                    v-model="formData.coop"
                    value="No"
                    checked="checked"
                  />
                  <label
                    v-if="formData.employment.includes('employ')"
                    class="form-check-label"
                    for="coop1"
                  >
                    No
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="coop"
                    v-model="formData.coop"
                    v-if="!formData.employment.includes('employ')"
                    value="No"
                    :disabled="formData.employment.includes('employed')"
                  />
                  <label
                    class="form-check-label"
                    v-if="!formData.employment.includes('employ')"
                    for="coop2"
                  >
                    No
                  </label>
                </div>
                <div
                  class="note"
                  v-show="formData.employment.includes('employ')"
                >
                  Funding for co-op programs is limited to students and recent
                  graduates.
                </div>
              </div>
              <div class="col-lg-6 pe-5 question">
                <label
                  :class="
                    'form-label' +
                    (formData.employment == 'Student' ? ' text-muted' : ' ')
                  "
                  >Are you looking for a position in the environmental sector
                  and available to work full-time, permanently?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="permanent"
                    id="permanent1"
                    v-model="formData.permanent"
                    value="Yes"
                    :disabled="formData.employment == 'Student'"
                  />
                  <label class="form-check-label" for="permanent1"> Yes </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="permanent"
                    id="permanent2"
                    v-model="formData.permanent"
                    value="No"
                    :disabled="formData.employment == 'Student'"
                  />
                  <label class="form-check-label" for="permanent2"> No </label>
                </div>
              </div>
            </div>
          </div>

          <div class="card p-4 rounded bg-light mt-5">
            <div class="col-lg-12 question">
              <h5 class="fw-bold form-label">
                Are you looking for support in any of the following? (check all
                that apply):
              </h5>
              <div class="form-check mt-4">
                <input
                  class="form-check-input"
                  type="checkbox"
                  name="lookingForSupport"
                  id="lookingForSupport1"
                  v-model="formData.support"
                  value="Demonstration of credibility as an environmental practitioner"
                />
                <label class="form-check-label" for="lookingForSupport1">
                  Demonstration of credibility as an environmental practitioner
                </label>
              </div>
              <div class="form-check mt-2">
                <input
                  class="form-check-input"
                  type="checkbox"
                  name="lookingForSupport"
                  id="lookingForSupport2"
                  v-model="formData.support"
                  value="Access to training and networking opportunities"
                />
                <label class="form-check-label" for="lookingForSupport2">
                  Access to training and networking opportunities
                </label>
              </div>
              <div class="form-check mt-2">
                <input
                  class="form-check-input"
                  type="checkbox"
                  name="lookingForSupport"
                  id="lookingForSupport3"
                  v-model="formData.support"
                  value="Enhance employment opportunities and growth"
                />
                <label class="form-check-label" for="lookingForSupport3">
                  Enhance employment opportunities and growth
                </label>
              </div>
            </div>
          </div>

          <div
            class="card p-4 rounded bg-light mt-5"
            v-show="
              formData.citizenship == 'Refugee' ||
              formData.citizenship == 'New Immigrant'
            "
          >
            <h5 class="card-title fw-bold">Immigrant Bridging</h5>

            <div class="row">
              <div
                class="col-lg-6 pe-5 question"
                :data-status="formData.IMM_graduation_status"
              >
                <label class="form-label"
                  >Have you graduated from a recognized post-secondary
                  institution with a 2-year diploma or 4-year degree?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_graduation_status"
                    v-model="formData.IMM_graduation_status"
                    id="IMM_graduation_status1"
                    value="Yes"
                  />
                  <label class="form-check-label" for="IMM_graduation_status1">
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_graduation_status"
                    id="IMM_graduation_status2"
                    v-model="formData.IMM_graduation_status"
                    value="No"
                  />
                  <label class="form-check-label" for="IMM_graduation_status2">
                    No
                  </label>
                </div>
              </div>

              <div class="col-lg-6 pe-5 question">
                <label class="form-label"
                  >Do you have international experience working in an
                  environmentally related capacity?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_international_experience"
                    id="IMM_international_experience1"
                    v-model="formData.IMM_international_experience"
                    value="Yes"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_international_experience1"
                  >
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_international_experience"
                    id="IMM_international_experience2"
                    v-model="formData.IMM_international_experience"
                    value="No"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_international_experience2"
                  >
                    No
                  </label>
                </div>
              </div>
              <div class="col-lg-6 pe-5 question">
                <label class="form-label"
                  >Do you have Canadian experience working in an environmentally
                  related capacity?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_canadian_experience"
                    id="IMM_canadian_experience1"
                    v-model="formData.IMM_canadian_experience"
                    value="Yes"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_canadian_experience1"
                  >
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_canadian_experience"
                    id="IMM_canadian_experience2"
                    v-model="formData.IMM_canadian_experience"
                    value="No"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_canadian_experience2"
                  >
                    No
                  </label>
                </div>
              </div>
              <div class="col-lg-6 pe-5 question">
                <label class="form-label"
                  >Do you have a Canadian Language Benchmark of 7 or
                  equivalent?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_language_benchmark"
                    id="IMM_language_benchmark1"
                    v-model="formData.IMM_language_benchmark"
                    value="Yes"
                  />
                  <label class="form-check-label" for="IMM_language_benchmark1">
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_language_benchmark"
                    id="IMM_language_benchmark2"
                    v-model="formData.IMM_language_benchmark"
                    value="No"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_canadian_experience2"
                  >
                    No
                  </label>
                </div>
              </div>
              <div class="col-lg-6 pe-5 question">
                <label class="form-label"
                  >Have you gone through any settlement programs or had any
                  appointments with a counselor from an immigrant-serving
                  agency?</label
                >
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_settlement_programs"
                    id="IMM_settlement_programs1"
                    v-model="formData.IMM_settlement_program"
                    value="Yes"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_settlement_programs1"
                  >
                    Yes
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="IMM_settlement_programs"
                    id="IMM_settlement_programs2"
                    v-model="formData.IMM_settlement_program"
                    value="No"
                  />
                  <label
                    class="form-check-label"
                    for="IMM_settlement_programs2"
                  >
                    No
                  </label>
                </div>
                <label
                  for="settlment_program_name"
                  class="form-label"
                  v-show="formData.IMM_settlement_program == 'Yes'"
                  >If yes, please specify the serving agency or settlement
                  program name</label
                >
                <input
                  type="text"
                  class="form-control"
                  id="settlment_program_name"
                  v-model="formData.IMM_settlement_program_name"
                  placeholder="Program Name"
                  v-show="formData.IMM_settlement_program == 'Yes'"
                />
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
          <div class="col my-3" :disabled="!formComplete">
            <Qualified
              id="eligibleBoth"
              v-if="
                formData.permanent == 'Yes' &&
                formData.coop == 'Yes' &&
                formComplete &&
                submit
              "
              text=' Thank you for your interest in our Employment Programs. Your
              answers in the pre-qualification form align with either:
              <div class="row text-center">
                <div class="col-12 p-3">
                  1) A full-time placement with a host organization.
                  <br />
                  <button
                    type="submit"
                    id="beginPermanentBoth"
                    class="
                      btn btn-success
                      mt-4
                      w-100
                      
                      shadow-sm
                      rounded-0
                    "
                  >
                    Begin Application
                  </button>
                </div>
                <div class="col-12 p-3">
                  2) a co-op work placement with a host organization.
                  <br />
                  <button
                    type="submit"
                    id="beginCoopBoth"
                    class="
                      btn
                      btn-success
                      mt-4
                      w-100            
                      shadow-sm
                      rounded-0
                    "
                  >
                    Begin Application
                  </button>'
            />

            <Qualified
              id="fullTime"
              v-if="
                formData.permanent == 'Yes' &&
                formData.coop == 'No' &&
                formData.citizenship != 'Refugee' &&
                formData.citizenship != 'New Immigrant' &&
                submit
              "
              link="#"
              text="Thank you for your interest in our Employment Programs. Your
              answers in the pre-qualification form align with a full-time
              placement with a host organization. Please click the button below
              to start your application."
            />
            <Qualified
              id="studentCoop"
              v-if="
                (formData.permanent == 'No' || formData.permanent == '') &&
                formData.coop == 'Yes' &&
                submit
              "
              link="#"
              text="Thank you for your interest in our Employment Programs. Your
              answers in the pre-qualification form align with a co-op work
              placement with a host organization. Please click the button below
              to start your application."
            />
            <Qualified
              id="immQualified"
              v-if="
                formData.IMM_graduation_status == 'Yes' &&
                formData.IMM_international_experience == 'Yes' &&
                formData.IMM_language_benchmark == 'Yes' &&
                (formData.citizenship == 'Refugee' ||
                  formData.citizenship == 'New Immigrant') &&
                submit
              "
              link="#"
              text="Thank you for your interest in our Employment Programs. Your
              answers in the pre-qualification form align with an Immigrant Bridging
              placement with a host organization. Please click the button below
              to start your application."
            />

            <Disqualified
              v-if="
                (formData.permanent.length == 0 ||
                  formData.permanent == 'No') &&
                (formData.coop.length == 0 || formData.coop == 'No') &&
                (formData.IMM_graduation_status !== 'Yes' ||
                  formData.IMM_international_experience !== 'Yes' ||
                  formData.IMM_language_benchmark !== 'Yes') &&
                submit
              "
              message='Thank you for your interest in our Employment Programs.
              Unfortunately, your answers in the pre-qualification form do not
              align with any of our offerings at this time. Please check back as
              we add more programs in the future. To browse available
              environmental jobs, check out our new
              <a href="/new-practitioners/employment-support/job-board/"
                >Job Board with AI-matching</a
              >'
            />
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
        birth_date: moment().subtract(30, "years").format("YYYY-MM-DD"),
        citizenship: "",
        employment: "",
        coop: "",
        permanent: "",
        support: [],
        IMM_graduation_status: "",
        IMM_international_experience: "",
        IMM_canadian_experience: "",
        IMM_settlement_program: "",
        IMM_settlement_program_name: "",
        IMM_language_benchmark: "",
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
    notCitizen() {
      if (
        this.formData.citizenship == "New Immigrant" ||
        this.formData.citizenship == "Refugee"
      ) {
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
        this.formData.birth_date &&
        this.formData.citizenship &&
        this.formData.employment &&
        (this.formData.coop ||
          this.formData.permanent ||
          this.formData.IMM_graduation_status)
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